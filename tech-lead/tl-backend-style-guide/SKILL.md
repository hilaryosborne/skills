---
name: tl-backend-style-guide
description: >
  Apply backend TypeScript conventions when generating, editing, or reviewing server-side code.
  Use when writing services, repositories, route handlers, domain models, error classes, or any
  non-React TypeScript. Covers module structure, class patterns, file naming, error handling,
  data access, and code style. This is a foundational skill - use it alongside more specific
  skills (e.g. database, Fastify) when those apply.
---

# Backend TypeScript Style Guide

When generating backend TypeScript code, follow these rules and patterns exactly.

## Environment

- TypeScript (strict)
- Native `fetch` for HTTP calls — never axios
- Zod for validation and schema definitions
- Direct imports — no dependency injection containers

## Module Structure

Backend code is organised into domain modules. Each module is a self-contained folder named `module.<domain>`, containing role-based sub-folders and files.

```
src/
  module.auth/
    auth.http/
      auth.http.routes.ts
      auth.http.login.handler.ts
      auth.http.register.handler.ts
    auth.service/
      auth.service.login.ts
      auth.service.register.ts
    auth.repository/
      auth.repository.user.ts
      auth.repository.session.ts
    auth.model/
      auth.model.user.ts
      auth.model.session.ts
    auth.error.ts
    auth.error.codes.ts
    index.ts
```

### Naming Convention

Every file and folder uses lowercase dot-notation: `<domain>.<role>.<specifics>.ts`

- Module folder: `module.auth`
- Sub-folders by role: `auth.http`, `auth.service`, `auth.repository`, `auth.model`
- Files within: `auth.service.register.ts`, `auth.http.login.handler.ts`
- Error files sit at module root: `auth.error.ts`, `auth.error.codes.ts`

### Sub-folder Rule

Every file belongs in a role-based sub-folder. The only files allowed at the module root are `index.ts` and the error files (`<domain>.error.ts`, `<domain>.error.codes.ts`). Everything else — constants, utilities, helpers, domain-specific concerns — goes in a sub-folder. If a set of files doesn't fit an existing role, create a new sub-folder for it. Even a single file gets its own sub-folder — the structure communicates intent.

```
// ✅ Correct — sourcing files in their own sub-folder
module.user/
  user.sourcing/
    user.aggregate.v1.ts
    user.events.v1.ts
    user.projection.account.v1.ts
  user.http/
    ...
  user.error.ts
  user.error.codes.ts
  index.ts

// ❌ Wrong — files dumped at module root
module.user/
  user.http/
    ...
  user.aggregate.v1.ts      ← should be in user.sourcing/
  user.events.v1.ts          ← should be in user.sourcing/
  user.projection.account.v1.ts  ← should be in user.sourcing/
  user.error.ts
  user.error.codes.ts
  index.ts
```

### Barrel Files

Every module has an `index.ts` that re-exports its public API. Consumers import from the module, not from internal files.

```ts
// module.auth/index.ts
export { default as AuthServiceLogin } from "./auth.service/auth.service.login";
export { default as AuthServiceRegister } from "./auth.service/auth.service.register";
export { default as AuthRepositoryUser } from "./auth.repository/auth.repository.user";
export { AuthError } from "./auth.error";
export { AuthErrorCode } from "./auth.error.codes";
export type { AuthModelUser } from "./auth.model/auth.model.user";
```

## Layer Responsibilities

### Handlers (arrow functions)

Route handlers are arrow functions. They parse the request, call services, catch domain errors, and return HTTP responses. Handlers can contain simple logic like input mapping or response shaping — they are not just pass-throughs.

```ts
// auth.http.login.handler.ts
import AuthServiceLogin from "../auth.service/auth.service.login";
import { AuthError } from "../auth.error";
import { AuthErrorCode } from "../auth.error.codes";

const loginHandler = async (request: Request): Promise<Response> => {
  try {
    const body = await request.json();
    const service = new AuthServiceLogin();
    const session = await service.execute(body.email, body.password);

    return Response.json({ session }, { status: 200 });
  } catch (error) {
    if (error instanceof AuthError) {
      if (error.code === AuthErrorCode.INVALID_CREDENTIALS) return Response.json({ error: error.message }, { status: 401 });
      if (error.code === AuthErrorCode.ACCOUNT_LOCKED) return Response.json({ error: error.message }, { status: 403 });
    }

    return Response.json({ error: "Internal server error" }, { status: 500 });
  }
};

export default loginHandler;
```

### Services (classes)

Services contain business logic. They orchestrate repositories, validate rules, and throw domain errors. Services never touch HTTP concepts (requests, responses, status codes). Instantiated with `new` by the consumer.

```ts
// auth.service.login.ts
import AuthRepositoryUser from "../auth.repository/auth.repository.user";
import { AuthError } from "../auth.error";
import { AuthErrorCode } from "../auth.error.codes";

class AuthServiceLogin {
  async execute(email: string, password: string) {
    const repository = new AuthRepositoryUser();
    const user = await repository.getByEmail(email);

    if (!user) throw new AuthError(AuthErrorCode.INVALID_CREDENTIALS, { email });
    if (user.status === "locked") throw new AuthError(AuthErrorCode.ACCOUNT_LOCKED, { email });

    // ... verify password, create session
    return session;
  }
}

export default AuthServiceLogin;
```

### Repositories (classes)

Repositories handle data access. They accept and return domain types — never raw database documents. Services never talk to the database directly. Instantiated with `new` by the consumer.

```ts
// auth.repository.user.ts
import type { AuthModelUser } from "../auth.model/auth.model.user";

class AuthRepositoryUser {
  async getByEmail(email: string): Promise<AuthModelUser | undefined> {
    // database-specific implementation
    const record = await db.collection("users").findOne({ email });
    return record ? record : undefined;
  }

  async create(user: AuthModelUser): Promise<AuthModelUser> {
    await db.collection("users").insertOne(user);
    const created = await db.collection("users").findOne({ uid: user.uid });
    if (!created) throw new Error("Failed to create user");
    return created;
  }
}

export default AuthRepositoryUser;
```

### Routes (controller)

The routes file registers all handlers for a domain's HTTP endpoints. This is the single entry point for the domain's HTTP surface.

```ts
// auth.http.routes.ts
import loginHandler from "./auth.http.login.handler";
import registerHandler from "./auth.http.register.handler";

// Framework-specific registration — details vary by router
const authRoutes = (router: Router) => {
  router.post("/auth/login", loginHandler);
  router.post("/auth/register", registerHandler);
};

export default authRoutes;
```

## Error Handling

Errors follow a strict two-file pattern per domain, plus a shared base error class.

### Base Error

A single `BaseError` class that all domain errors extend. Lives outside any module (e.g. `src/error/base.error.ts`).

```ts
// error/base.error.ts
class BaseError extends Error {
  constructor(
    public code: string,
    message?: string,
    public context?: Record<string, unknown>,
    public original?: unknown,
  ) {
    super(message);
    Object.setPrototypeOf(this, new.target.prototype);
    this.name = this.constructor.name;
    Error.captureStackTrace(this, this.constructor);
  }
}

export default BaseError;
```

### Domain Error Class

Each domain has an error class extending `BaseError`. The class resolves the human-readable message from the error code automatically.

```ts
// auth.error.ts
import BaseError from "@/error/base.error";
import { AuthErrorCode, AuthErrorMessage } from "./auth.error.codes";

export class AuthError extends BaseError {
  constructor(
    public code: AuthErrorCode,
    public context?: Record<string, unknown>,
    public original?: unknown,
  ) {
    super(code, AuthErrorMessage[code], context, original);
  }
}
```

### Domain Error Codes

A `const enum` of all error codes and a `Record` mapping each code to a human-readable message. All error codes for the domain live in one file.

```ts
// auth.error.codes.ts
export enum AuthErrorCode {
  INVALID_CREDENTIALS = "AUTH_INVALID_CREDENTIALS",
  ACCOUNT_LOCKED = "AUTH_ACCOUNT_LOCKED",
  ACCOUNT_NOT_FOUND = "AUTH_ACCOUNT_NOT_FOUND",
  SESSION_EXPIRED = "AUTH_SESSION_EXPIRED",
  TOKEN_INVALID = "AUTH_TOKEN_INVALID",
}

export const AuthErrorMessage: Record<AuthErrorCode, string> = {
  [AuthErrorCode.INVALID_CREDENTIALS]: "Invalid email or password",
  [AuthErrorCode.ACCOUNT_LOCKED]: "Account is locked",
  [AuthErrorCode.ACCOUNT_NOT_FOUND]: "Account not found",
  [AuthErrorCode.SESSION_EXPIRED]: "Session has expired",
  [AuthErrorCode.TOKEN_INVALID]: "Token is invalid",
};
```

### Throwing Errors

Services throw domain errors with the code and optional context. The handler catches and maps to HTTP responses.

```ts
// In a service — throw with code + context
throw new AuthError(AuthErrorCode.ACCOUNT_NOT_FOUND, { email });

// In a handler — catch and map
if (error instanceof AuthError) {
  if (error.code === AuthErrorCode.ACCOUNT_NOT_FOUND) return Response.json({ error: error.message }, { status: 404 });
}
```

## Data Models

- Define with `type` (not `interface`)
- Single-word property names wherever possible
- Nested objects over compound names — prefer depth for flexibility

```ts
// ✅ Preferred
type AuthModelUser = {
  uid: string;
  name: { first: string; last: string };
  contact: {
    emails: { primary: string; all: { address: string; verified: boolean }[] };
  };
  status: "active" | "locked" | "suspended";
};

// ❌ Avoid
type AuthModelUser = {
  uid: string;
  firstName: string;
  primaryEmail: string;
  emailVerified: boolean;
};
```

## File Export Rules

- Every file has a single default export — this is the file's purpose
- Classes are the default export for services and repositories
- Arrow functions are the default export for handlers
- Named exports are reserved for supporting types, enums, and constants
- Barrel `index.ts` files re-export from the module root

## File Internal Order

1. Imports
2. Types — local types at the top of the file body
3. Implementation — the class or function body
4. Export — `export default` at the bottom

## Code Style

- TypeScript strict mode
- `type` over `interface` for all type definitions
- Minimal comments — code is self-documenting through clear naming
- Single-line conditionals omit `{}` and stack vertically:

```ts
if (user.role === "admin") return true;
else if (user.role === "editor") return true;
else if (user.role === "viewer") return false;
else return false;
```

- Always `return undefined` explicitly, never bare `return`:

```ts
// ✅
if (!user) return undefined;

// ❌
if (!user) return;
```

- Ternaries returning the input or `undefined` are fine:

```ts
return record ? record : undefined;
```

- No semicolons at end of lines unless the project's existing config requires them — follow whatever the project already uses
- Prefer `async/await` over `.then()` chains
