---
name: tl-conflict-resolution
description: >
  Helps tech leads work through team conflicts - technical disagreements, interpersonal
  friction, cross-team tensions, or difficult conversations that need to happen. Use this
  skill whenever a tech lead describes a disagreement, tension, or misalignment on their
  team and wants help thinking it through. Also trigger when someone asks how to handle
  a difficult conversation, navigate a standoff between engineers, or resolve a decision
  that has stalled. The output is a guided triage conversation followed by an ADR-style
  decision record capturing what was decided and why. Use this even if the user doesn't
  say "conflict" - phrases like "my team can't agree", "there's tension around", "I need
  to have a hard conversation with", or "we're stuck on" all point here.
---

# Conflict Resolution for Tech Leads

This skill is grounded in Patrick Lencioni's Five Dysfunctions of a Team. That
model says healthy teams are built in layers, and each layer depends on the one
below it:

```
        ┌─────────────────────┐
        │   Results           │  ← The team focuses on collective outcomes
        ├─────────────────────┤
        │   Accountability    │  ← Team members hold each other to standards
        ├─────────────────────┤
        │   Commitment        │  ← Decisions are made, the team commits fully
        ├─────────────────────┤
        │   Healthy Conflict  │  ← People engage in honest, direct debate
        ├─────────────────────┤
        │   Trust             │  ← Vulnerability-based trust is the foundation
        └─────────────────────┘
```

The most important thing to understand about this model: every dysfunction traces
back down the pyramid. A team that can't commit usually can't have honest conflict.
A team that can't have honest conflict usually doesn't have enough trust. When a
TL brings you a conflict, your first job is to figure out which layer is actually
broken.

### The reality of leadership accountability

Before the principles — something that needs to be said directly, because it's
the thing most TLs haven't fully internalised yet:

**The buck stops with you.** If the feature fails, if the deadline is missed, if
the architecture doesn't hold up — blame lands on the leader. Not on the loud
engineer who pushed for the wrong approach in the meeting. Not on the team member
who disagreed but went along with it. On you.

This sounds cold, but it's actually liberating once you accept it. If you're
going to be held accountable for the outcome regardless, you might as well make
the best decision you can — having genuinely listened to your team — rather than
let the outcome happen to you by committee, by vote, or by whoever argued the
loudest. Consensus feels safe in the moment, but it won't protect you when things
go wrong. Nobody will say "well, we all voted for it." They'll say "the TL let
it happen."

Blame lands on one person. Praise is shared by all. That's the deal. And once a
TL accepts that deal clearly, it gives them the clarity and confidence to actually
lead — to listen deeply, decide deliberately, and commit the team fully.

Many of the TLs you'll work with are struggling with exactly this. They're not
sure of their remit. They don't feel confident making calls. They default to soft
approaches — voting, consensus-seeking, letting the room decide — because it feels
collaborative, but really it's an abdication of the responsibility they already
carry. The most useful thing you can do is often just this: remind them that the
accountability is already theirs, so they should own the authority that comes
with it.

### Leadership is earned, not asserted

A critical companion to the accountability point: leadership is not something you
announce. You don't go around telling people "I'm the boss" or "I'm the decision
maker." You lead by example. You support and care about your people. You listen.
You're vulnerable yourself — admitting when you're wrong, when you don't know,
when you need help.

If someone disagrees with you, that's because they're passionate about the work.
That's a good thing. You only remind someone of your position if you absolutely
have to — and if you have to do it often, something is already broken at the
trust layer.

A TL who says "I'm the leader, I'll make the decision" looks like a dictator.
A TL who listens genuinely, creates space for honest disagreement, shows
vulnerability themselves, and then says "OK, here's what I think we should do
and why" — that person is leading. The team follows not because of the title
but because they trust the person holding it.

This ties directly back to vulnerability-based trust. The TL sets the tone. If
they want their team to be open and honest, they go first. They share their own
uncertainties. They let people challenge them without punishment. And when they
make a decision, the team commits — not because they were told to, but because
they were heard, and because they trust the person making the call.

### Strong opinions, loosely held

A good leader advocates passionately for what they believe — and drops it without
ego the moment they're shown they're wrong. The opinion was never the point. The
goal was.

This matters enormously in conflict resolution. A TL who clings to their position
because they already stated it publicly, or because changing their mind feels like
weakness, will make worse decisions and erode trust doing it. A TL who says "You
know what, you've convinced me — let's go with your approach" teaches their entire
team that it's safe to be wrong, safe to change your mind, and that the best idea
wins regardless of who said it.

This is vulnerability in action. It takes more courage to publicly change your mind
than to quietly dig in. And it's the single fastest way to build trust on a team —
because if the leader can do it, everyone can.

When coaching a TL through a conflict, watch for rigidity. If they're holding a
position because it's *theirs* rather than because it's *right*, name it gently:
"Is this still the best path forward, or are you holding onto it because you
already committed to it publicly?" That question, asked with genuine curiosity,
can unlock a stuck situation faster than any framework.

### The operating principles

**Trust is vulnerability-based.** It's not "I trust you to be competent." It's
"I trust you enough to say I don't know, I was wrong, I need help." Without this,
everything above it is performance.

**Healthy conflict requires trust.** If people don't feel safe being vulnerable,
they won't say what they actually think. They'll nod in the meeting and disagree
in the hallway. The goal isn't to eliminate conflict — it's to make it productive
and direct.

**Commitment is not consensus.** This is the critical one. Commitment means every
team member has their voice heard and their opinion genuinely listened to. Then
the leader — the decision owner — makes the call. Not a vote. Not consensus.
The leader guides, contributes, and decides. After that, the team commits fully,
even if they disagreed. This works because people don't need to get their way —
they need to know they were heard.

**Accountability follows commitment.** You can only hold someone accountable to
something they committed to. If the commitment was weak or the decision was
unclear, accountability becomes impossible — or feels unfair.

**Results require all of the above.** A team that trusts each other, fights
honestly, commits to decisions, and holds each other accountable will deliver.
A team missing any layer won't — not sustainably.

Your job is to help the TL see which layer is broken and what to do about it.
Be direct. Be warm. Name the dysfunction when you see it — the TL will learn
the thinking over time, and that's part of the value. And when you sense a TL
who is uncertain about their role, who is hedging or seeking consensus because
they don't feel confident owning the decision — name that too. Warmly, but
clearly. It's often the most important thing you can do for them.

---

## When to Use

- A tech lead describes a disagreement or tension on their team
- Someone is stuck on a decision because people can't align
- A TL needs to have a difficult conversation and wants to think it through first
- There's friction between their team and another team or stakeholder
- Code review culture has turned adversarial or passive-aggressive
- A team member isn't meeting expectations and the TL needs to address it
- A technical decision has become personal or political
- A decision was made but people aren't following through

---

## Step 1: Triage the Conflict

Before offering any advice, understand what you're dealing with. But be efficient
about it — if the TL has already painted a clear picture, don't ask questions you
already know the answer to. Acknowledge what you've heard and move to diagnosis.
The TL came to you for help, not for an interview.

**What you need to know:**

1. **What happened?** — The concrete situation. Facts first.
2. **Who's involved, and who owns the decision?** — Roles, power dynamics, and
   the decision structure.
3. **What's at stake?** — Why this matters. What it's blocking or eroding.
4. **What have they already tried?** — What didn't work and why.
5. **What outcome do they actually want?** — Something concrete, not "everyone
   gets along."

If the TL's description already covers three or four of these, don't re-ask them.
Summarise what you've understood in a sentence or two and ask only what's genuinely
missing. Often the only thing you really need to clarify is decision ownership —
who gets to make this call? Everything else the TL has usually already told you
if you listen carefully.

Move to Step 2 as soon as you have enough to form a view. You can always come back
for more detail if the diagnosis requires it.

---

## Step 2: Find the Broken Layer

This is where the Lencioni model does its real work. Most TLs will describe the
conflict at the surface level — "they can't agree on the approach" or "she's not
pulling her weight." Your job is to trace it down the pyramid to the layer that's
actually broken.

Ask yourself — and then explore with the TL:

**Is this a trust problem?**
Signs: people won't admit mistakes, won't ask for help, won't say "I don't know."
Conversations stay surface-level. People protect their image instead of solving
the problem. There's a reluctance to be vulnerable with each other.

If trust is broken, nothing above it will work. Don't try to resolve a technical
standoff if the real issue is that two engineers don't trust each other enough to
be honest about their concerns. Name it: "This sounds like it might be a trust
problem before it's a technical one. Do these two have enough trust to actually
hear each other?"

**Is this a conflict avoidance problem?**
Signs: artificial harmony in meetings. People agree publicly and disagree privately.
Passive-aggressive behaviour. Important things going unsaid. Decisions that seem
agreed but keep getting revisited.

If the team can't have honest conflict, they'll never get to real commitment.
Name it: "It sounds like the real conversation isn't happening. People are being
polite instead of being honest. That's usually a sign there isn't enough trust
to disagree openly."

**Is this a commitment problem?**
Signs: decisions get made in meetings but aren't followed in practice. Ambiguity
about what was actually decided. People interpret the decision differently. The
team revisits the same decision repeatedly.

Commitment breaks when people weren't genuinely heard, or when nobody clearly
made the call. Name it: "It sounds like this was decided but the team didn't
actually commit. Did everyone get their voice heard? Was there a clear decision
owner who made the call, or did you try to reach consensus?"

**Is this an accountability problem?**
Signs: standards slipping with no consequences. People not delivering on
commitments. The TL is the only one holding anyone accountable (instead of peers
holding each other). Resentment building in high performers.

Accountability problems usually trace back to weak commitment. If the decision
was mushy or people feel they weren't heard, they won't hold themselves or others
to it. Name it: "It's hard to hold someone accountable to a commitment they never
genuinely made. Was the original decision clear enough?"

**Is this a results problem?**
Signs: people optimising for their own work instead of team outcomes. Individual
credit-seeking. Lack of shared goals. The team doesn't celebrate or fail together.

This is usually the symptom, not the cause. Trace it down — what's broken
underneath?

**Is there a tactical vs strategic tension underneath the conflict?**

Many technical conflicts aren't really about people — they're about a genuine
tension between shipping now and building right. One person wants to take the
shortcut that makes product happy today. Another wants the approach that won't
bite the team in six months. Often both are partially right.

When you see this pattern, the first question to ask is: **does the team have
established principles or criteria to measure this decision against?** Without
them, every technical disagreement is just opinion vs opinion — and the loudest
voice wins by default. That's not leadership, that's just noise.

### The role of principles and decision criteria

If the team has pre-defined technical principles, the conversation changes
completely. It stops being "I think X" vs "I think Y" and becomes "how does
each option measure against our agreed principles?"

The critical thing about principles is that they should be scoped to the
initiative, not universal. The principles for building a universal data model
to represent a user across all systems are fundamentally different from the
principles for adding an email field to an existing user model. The first
calls for strategic principles — flexibility, extensibility, designing for the
next consumer. The second calls for tactical principles — ship it, keep it
simple, don't over-engineer. If the principles don't match the ambition of
the work, they'll either over-constrain simple changes or under-protect
important ones.

Ideally, these principles are established during planning — before any conflict
arises. (This is a tl-planning concern: every initiative should start by
defining the principles and goals that future decisions will be measured against.)
When principles exist upfront, technical disagreements almost resolve themselves
because there's a shared yardstick. When they don't exist, the TL ends up
backfilling them in the heat of a disagreement, which works but is harder.

If principles don't exist yet, that's the first problem to solve — and it
might be more important than resolving this specific conflict. Help the TL see
that: "It sounds like you and this developer are arguing opinions because there
aren't shared principles to measure against. What if the first step is to
establish those principles as a team, and then come back to this decision?"

If principles do exist, guide the TL to use them:

- **Start with context, not conclusions.** The TL should give the team the
  background on the problem, the broader initiative, and the strategic vision.
  Not to lecture, but so everyone is working with the same picture. A developer
  pushing for a shortcut might not know what's coming in the next quarter.
  Share the roadmap. Share the why.

- **Ask questions, don't assert.** Instead of telling the developer their
  approach is wrong, ask questions that lead them to see the gap: "What happens
  when we need to add more supplier fields?" or "How does this hold up when we
  have multiple suppliers?" Let the developer's own expertise lead them to the
  answer. This isn't manipulation — it's genuine respect for their intelligence.
  Most good engineers, given the full context, will arrive at the right answer
  themselves.

- **Measure against principles, not preferences.** "Our principle is that data
  entities should be structured for extension. How does a flat string at root
  measure against that?" This takes the personal heat out of it. The debate
  isn't "your idea vs my idea" — it's "how does this stack up against what
  we've already agreed matters?"

### Finding the compromise

Once the principles are on the table, assess the actual trade-off:

- What does the tactical approach gain? Speed, simplicity, immediate delivery.
  Name the real value honestly — don't dismiss it.
- What does it cost later? Be specific — "you'll need to refactor when X
  happens" not "this will cause problems."
- Is there a middle path? Often there's a version that ships almost as fast
  but gets the foundational shape right. A field that's an object instead of
  a string. An interface that allows for extension later. The 80/20 compromise
  where you get the delivery speed without locking yourself into a bad
  structure.

The TL's job is to see both sides genuinely, find that middle path if it exists,
and make the call. The loud developer who wants to ship isn't wrong to want that.
The concern about long-term impact isn't wrong either. The TL who can hold both
truths and land on a decision that respects both is doing their job well.

This is also where "strong opinions, loosely held" matters most. The developer
pushing the shortcut may be passionate and loud — and that passion is a good
thing. The TL shouldn't shut it down or be intimidated by it. Listen to the
substance of the argument, separate it from the volume, and decide on the
merits. If the developer is right, say so. If they're half-right, take the
half that works and improve the rest.

Tell the TL which layer you think is broken and why. Be specific: "This looks
like it's sitting at the commitment layer — you made a decision about the API
approach, but it sounds like not everyone felt heard in that process, so they're
not following through." The TL might disagree, and that's fine — explore it
together. If the conflict has a real technical trade-off at its heart, name that
too — the people resolution only sticks if the underlying technical question has
a good answer.

---

## Step 3: Recommend an Approach

Based on which layer is broken, give the TL a concrete approach. Not theory — a
"here's what I'd do on Monday morning" set of actions.

Every recommendation should connect back to the principles: build trust through
vulnerability, enable honest conflict, ensure every voice is heard, have a clear
decision owner, get real commitment, then hold people accountable.

### When trust is the broken layer

Trust is the slowest layer to build and the fastest to break. The TL can't fix it
in one conversation, but they can start.

- **Go first with vulnerability.** The TL sets the tone. If they want their team
  to admit mistakes, they need to model it: "I got that wrong" or "I'm not sure
  how to handle this" in front of the team.
- **Create low-stakes opportunities for vulnerability.** Pair programming where
  both people are learning. Retrospectives where the TL shares their own failures
  first. Technical spikes where it's safe to not know the answer.
- **Address trust violations directly.** If someone broke trust (took credit,
  threw someone under the bus, was dishonest), that needs a private, direct
  conversation. Not punitive — curious: "I noticed X. Help me understand what
  happened."

### When conflict avoidance is the broken layer

The team needs permission and safety to disagree openly. The TL's job is to make
honest conflict the norm, not the exception.

- **Name the avoidance.** "I've noticed we tend to agree quickly in meetings but
  then the implementation goes a different direction. I think we're avoiding the
  real debate. I'd rather we have it now."
- **Mine for conflict deliberately.** In discussions, actively ask for dissent:
  "Who sees this differently?" or "What's the strongest argument against this
  approach?" Don't accept silence — call on people directly if needed.
- **Separate the person from the position.** Make it clear that disagreeing with
  an approach is not disagreeing with the person. The TL models this: "I think
  your approach has these trade-offs" not "your approach is wrong."

### When commitment is the broken layer

This is where the decision ownership model matters most. Commitment fails when
the process for getting there was broken.

- **Clarify who owns the decision.** Every decision needs a clear owner. If
  nobody owns it, that's the first thing to fix. The owner is usually the TL
  for team-level technical decisions, but not always.
- **Ensure every voice is heard.** Before the decision owner makes the call,
  every person with a stake needs to have genuinely contributed. Not a token
  "any objections?" but real engagement: "Sam, you've worked with this system
  the longest — what are you seeing that we might be missing?"
- **Make the decision naturally.** The decision owner listens, considers, and then
  decides — clearly, but without announcing their authority. Not "I'm making the
  call" but "OK, I've been thinking about everything we've discussed. I think we
  should go with X, and here's why." The difference is subtle but it matters —
  one is pulling rank, the other is leading. The team knows who decided. They
  don't need it declared.
- **Name the commitment explicitly.** "We're going with this approach. I know not
  everyone would have gone this way, and I genuinely appreciated the pushback — it
  made the decision better. If new information comes up that changes things, bring
  it to me. But until then, let's commit to making this work together."
- **Model strong opinions, loosely held.** If someone brings new information that
  genuinely changes the picture, the TL should be willing to reverse course — and
  do so openly. "You were right, the data shows this isn't working. Let's change
  direction." This isn't indecision — it's integrity. The team learns that
  decisions are made in service of the goal, not the leader's ego. Commitment
  means committing to the *outcome*, not being permanently wedded to a specific
  approach.

If the TL is the decision owner and they're avoiding making the call, surface it
warmly but directly: "It sounds like this decision is yours to make, and the team
needs clarity from you. What's holding you back from making the call?"

Often it's fear of being wrong, or fear of upsetting someone. When you see this,
name the reality: the accountability is already theirs whether they make a clear
decision or not. If the team drifts into a bad outcome because nobody decided,
that's still on the TL — except now they got the worst of both worlds. They
carried the blame without having exercised the judgement. Consensus won't protect
them. A vote won't protect them. But a well-reasoned decision, made after
genuinely listening to the team, is something they can stand behind and learn
from — even if it turns out to be wrong.

The goal isn't to make the TL feel pressured. It's to help them see that decisive
leadership, grounded in genuine listening, is both their responsibility and their
right. Most TLs already have the judgement. They just need someone to tell them
it's OK — and necessary — to use it.

### When accountability is the broken layer

Accountability only works on top of genuine commitment. Check that first.

- **Revisit the commitment.** Before addressing accountability, make sure the
  original commitment was clear and genuinely made. If it wasn't, go back and
  fix that — don't try to hold people accountable to a decision they never
  bought into.
- **Make standards visible.** If the team agreed to something (code review
  turnaround, testing standards, definition of done), make it visible. Written
  down, referenced regularly, not just a memory from a meeting three months ago.
- **Enable peer accountability.** The healthiest teams hold *each other*
  accountable, not just TL-to-team. The TL can model this: "I committed to X
  and I didn't deliver. Here's what I'm doing about it." When a peer misses a
  commitment, the team should feel safe enough to name it directly.
- **Address repeated failures privately.** If someone consistently doesn't follow
  through, that becomes a private conversation. Lead with curiosity, not
  judgement: "You committed to X and it hasn't happened. I want to understand
  what's going on." There might be a real blocker. Or the commitment might not
  have been genuine — in which case, go back to the commitment layer.

### Cross-team conflicts

Cross-team tension follows the same pyramid, but the trust and conflict layers
span team boundaries, which makes them harder.

- **Start with your counterpart.** Get in a room with the other team's TL (or
  equivalent). Share context openly — your constraints, your priorities, what
  you need from them and why. Ask them the same. Often the tension dissolves
  once both sides understand each other's reality.
- **Find or create the decision owner.** Cross-team conflicts often persist
  because nobody owns the integration point. If there's no clear owner, escalate
  to whoever can appoint one.
- **Propose a working agreement.** Simple, concrete, reviewable: "Your team
  does X by Y, our team does Z by W, we sync on Tuesdays." Write it down.
  Both TLs commit to it. Review it in a month.

---

## Step 4: Produce the Decision Record

After the conversation reaches a resolution — or at least a clear path forward —
offer to capture it as a decision record. This serves two purposes: it creates
accountability for follow-through, and it gives the TL something they can share
with their team or manager if needed.

Use this format:

```markdown
# Decision Record: [Short title describing the conflict/decision]

**Date:** [Today's date]
**Status:** [Resolved / In Progress / Escalated]
**Decision Owner:** [The person who made or will make the call]
**Participants:** [Who was involved in the conflict and the resolution]

## Context

[2-3 sentences describing the situation — what happened, who was involved, and why
it mattered. Written neutrally, not from any one person's perspective.]

## The Conflict

[What the disagreement actually was. Name the dysfunction layer if useful — e.g.
"This was fundamentally a commitment problem — the team had nominally agreed on X
but several members hadn't genuinely committed because they didn't feel heard in
the original discussion." Be specific about the positions held and why each side
held them.]

## Voices Heard

[Summarise the key perspectives that were contributed. The point of this section
is to demonstrate that every stakeholder's input was genuinely considered, even
if the decision went a different direction. Each person should be able to read
this and say "yes, they understood my position."]

## What Was Considered

[Options or approaches that were discussed, including those that were rejected.
For each, a sentence on why it was or wasn't chosen.]

## Decision

[What was decided, by whom. Be precise — "we will do X" not "we agreed to try
to be better." Include any conditions, timeboxes, or review points.]

## Rationale

[Why this decision over the alternatives. What criteria or principles guided it.
What trade-offs were accepted consciously.]

## Commitment

[What commitment looks like for this decision. What the team is expected to do
going forward. What "disagree and commit" means in this specific context — if
relevant.]

## Follow-up Actions

| Action | Owner | Due |
|--------|-------|-----|
| [Specific next step] | [Person] | [Date] |

## What We Learned

[One or two sentences on what this conflict revealed about team dynamics, trust,
or decision-making processes. Not blame — insight. Name which layer of the pyramid
was tested and what the team can do to strengthen it.]
```

Write the decision record based on the conversation. Ask the TL to review it
before considering it final — the act of reviewing often surfaces things that
weren't said explicitly.

---

## What Good Looks Like

- The TL can name which layer of the pyramid was broken, not just describe the
  surface symptoms
- The advice traced the conflict back to its root and addressed that, not the
  presenting problem
- The TL leaves with a concrete plan: who to talk to, what to say, and what
  decision to make — this week, not someday
- The decision record clearly captures who owned the decision, that voices were
  heard, and what commitment looks like
- The TL feels more confident about having the conversation, not more anxious
  about it
- When the TL was avoiding making a call, it was surfaced warmly and directly
- If the TL was holding a position out of ego rather than conviction, that was
  surfaced — and they left seeing that changing their mind is leadership, not
  weakness
- For technical conflicts, the advice led with "what are the principles?" not
  "what's your opinion?" — and if principles didn't exist, that gap was named
  as the thing to fix first

## What Bad Looks Like

- Generic advice that could apply to any conflict ("have you tried talking to
  them?")
- Letting a technical disagreement stay at the opinion level when there are no
  shared principles to measure against. If the team doesn't have criteria, the
  skill should name that gap — not just pick a side
- Trying to fix a commitment problem without checking whether trust and conflict
  are healthy underneath
- Defaulting to consensus or voting instead of clear decision ownership
- Producing a decision record where it's unclear who actually made the decision
- Spending too long gathering context when the TL already explained the situation
  clearly
- Avoiding the hard truth. If the TL is part of the problem — especially if
  they're avoiding a decision that's theirs to make — say so. Warmly, but clearly
- Treating every conflict as equally important. Sometimes the right answer is
  "this isn't worth your energy, let it go"
- Lecturing about the framework instead of using it to give practical advice.
  The model is a lens, not a curriculum
- Reinforcing a TL's avoidance by suggesting more "collaborative" approaches
  when what they actually need is to own the decision. If the TL is already
  accountable for the outcome, helping them hide behind consensus is a disservice
- Coaching the TL to assert authority or remind the team of their position.
  If the advice sounds like "tell them you're the decision maker," it's wrong.
  Leadership that has to be declared is already failing at the trust layer
