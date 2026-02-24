---
name: tl-react-style-guide
description: >
  Apply React component conventions when generating, editing, or reviewing React code.
  Use when writing React components, hooks, types, data models, or file structures.
  Covers component definition, composition patterns, file naming, props, data fetching,
  styling, and code style.
---

# React Component Style Guide

When generating React components, follow these rules and patterns exactly.

## Framework & Environment

- Next.js App Router
- TypeScript (strict)
- Most components are client components (`'use client'`)
- Tailwind CSS for styling — direct `className` strings

## Component Definition

- Arrow functions with default export
- Props typed with `type` (not `interface`)
- Props destructured directly in function parameters

## Props Pattern

Every component includes:
- An optional `className` prop merged using the `classnames` library
- An index signature `[key: string]: unknown` for data attributes
- Rest props spread onto the root element

```tsx
export type UserCardProps = {
  className?: string
  [key: string]: unknown
}

const UserCard = ({ className, ...props }: UserCardProps) => {
  return (
    <div className={classNames('rounded-lg border p-4', className)} {...props} />
  )
}

export default UserCard
```

## File Naming & Structure

- All filenames are always **lowercase** — no uppercase letters ever
- Dot-notation file names: `context.component.name.tsx`
  - Examples: `user.auth.form.tsx`, `dashboard.stats.card.tsx`, `user.card.skeleton.tsx`
- Hooks follow the same convention with `use-` prefix: `cart.use-checkout.ts`
- Helper functions get their own file: `user.format-name.ts`

## File Export Rules

- Every file has a single default export — this is the file's purpose
- One function, component, or hook per file
- Named exports are reserved for supporting internals (props types, Zod schemas)
- Importing a named export signals accessing something internal to that file

```tsx
// user.card.username.tsx

export type UserCardUserNameProps = {
  variant?: 'full' | 'short'
  className?: string
  [key: string]: unknown
}

const UserCardUserName = ({ variant = 'full', className, ...props }: UserCardUserNameProps) => {
  const user = useUser()
  const display = variant === 'full'
    ? `${user.name.first} ${user.name.last}`
    : user.username

  return <span className={classNames('text-sm font-medium', className)} {...props}>{display}</span>
}

export default UserCardUserName
```

## File Internal Order

1. Types — prop types and local types at the top
2. Component — the arrow function body
3. Export — `export default` at the bottom

## Component Architecture

Use compound component composition:
- Single-purpose standalone components — each does one thing
- Context providers per entity to avoid prop drilling
- Leaf components pull their own data from context via hooks
- A composition component assembles the view from individual pieces

```tsx
const UserList = ({ className, ...props }: UserListProps) => {
  const users = [
    { username: 'Alice', age: 30, email: 'alice@example.com' },
    { username: 'Bob', age: 25, email: 'bob@example.com' },
  ]

  return (
    <UserListContainer className={className} {...props}>
      {users.map((user, index) => (
        <UserProvider key={index} value={user}>
          <UserCard>
            <UserCardHeader>
              <UserCardIcon />
              <UserCardUserName />
              <UserCardEmail />
            </UserCardHeader>
            <UserCardBody>
              <UserCardAge />
            </UserCardBody>
          </UserCard>
        </UserProvider>
      ))}
    </UserListContainer>
  )
}
```

### Breakdown:
- `UserProvider` — context provider wrapping each entity
- `UserCard`, `UserCardHeader`, `UserCardBody` — structural/layout components
- `UserCardUserName`, `UserCardEmail`, `UserCardAge` — leaf components that pull data from context via `useUser()`
- `UserList` — composition component that orchestrates the view

## Loading States

Use skeleton components for async fetches that mirror the real component layout:
- Simple views get a single skeleton component
- Complex views compose from shared skeleton sub-components

```tsx
// user.card.skeleton.tsx
const UserCardSkeleton = () => {
  return (
    <div className="flex items-center gap-4 rounded-lg border p-4 animate-pulse">
      <div className="h-10 w-10 rounded-full bg-gray-200" />
      <div className="flex flex-col gap-2">
        <div className="h-4 w-24 rounded bg-gray-200" />
        <div className="h-3 w-32 rounded bg-gray-200" />
      </div>
    </div>
  )
}

export default UserCardSkeleton
```

```tsx
// user.list.skeleton.tsx
const UserListSkeleton = () => {
  return (
    <UserListContainer>
      {Array.from({ length: 3 }).map((_, index) => (
        <UserCardSkeleton key={index} />
      ))}
    </UserListContainer>
  )
}

export default UserListSkeleton
```

Separate components for error and empty states as well.

## Data Models

- Single-word property names wherever possible
- Nested objects over compound names — prefer depth for flexibility

```tsx
// Preferred
type User = {
  username: string
  name: { first: string; last: string; middle?: string; suffix?: string }
  address: {
    street: { name: string; number: number; type: string }
    city: { name: string; population: number }
  }
}

// Avoid
type User = {
  username: string
  firstName: string
  streetName: string
  cityName: string
}
```

## Context Providers

Context files follow a strict structure. Entity types (e.g. `Flight`, `User`) are imported from their own files — never defined in the context file.

### Types

Three types are always defined in this order:

- `EntityContextState` — the data shape stored in state
- `EntityContextValue` — extends state, adds setters and actions
- `EntityProviderProps` — includes `children: React.ReactNode`, any seed props, and the index signature

```tsx
export type FlightContextState = {
  flight: Flight | null
}

export type FlightContextValue = FlightContextState & {
  setFlight: (flight: Flight) => void
}

export type FlightProviderProps = {
  value: Flight
  children: React.ReactNode
  [key: string]: unknown
}
```

### Context Object

- Created with `createContext` typed with `ContextValue`
- Defaults are sensible: `null` for data, no-ops for setters
- Named export (not default)

```tsx
export const FlightContext = createContext<FlightContextValue>({
  flight: null,
  setFlight: () => {},
})
```

### Context Hook

- Co-located in the same file as the provider
- Always includes a guard that throws if used outside the provider
- Named export

```tsx
export const useFlightContext = () => {
  const ctx = useContext(FlightContext)
  if (!ctx) throw new Error('useFlightContext must be used inside FlightProvider')
  return ctx
}
```

### Provider Component

- Internal `useState` typed with `ContextState` (not `ContextValue`)
- Setters and actions defined inside the component body
- Provider value always lists fields explicitly — never spreads state directly
- Initialisation is flexible — state may be seeded from props, fetched, calculated, or a mix
- Default export

```tsx
const FlightProvider = ({ value, children }: FlightProviderProps) => {
  const [state, setState] = useState<FlightContextState>({ flight: value })
  const setFlight = (flight: Flight) => setState({ flight })
  return (
    <FlightContext.Provider value={{ flight: state.flight, setFlight }}>
      {children}
    </FlightContext.Provider>
  )
}

export default FlightProvider
```

## Data Fetching

- TanStack Query for server state
- Native `fetch` when TanStack Query isn't needed

## Validation

- Zod for form validation and schema definitions

## Custom Hooks

- Extracted to separate files, never inline in components
- Dot-notation naming with `use-` prefix: `cart.use-checkout.ts`
- **Exception**: Context hooks are co-located with their provider file — the hook is the consumer API for that context and is tightly coupled to it

## Code Style

- Minimal comments — code is self-documenting through clear naming
- Memoization is rarely used — only for real performance issues
- Never use `<></>` shorthand — always use `<React.Fragment></React.Fragment>` explicitly
- Single-line conditionals omit `{}` and stack vertically:

```tsx
if (user.group === 'admin') return true
else if (user.group === 'editor') return true
else if (user.group === 'viewer') return false
else return false
```

- Always `return undefined` explicitly, never bare `return`:

```tsx
// Preferred
if (!user) return undefined

// Avoid
if (!user) return
```
