# /zoom

Trigger: user types `/zoom`, "zoom out", "give me the big picture", "I don't know this area", "map this out".

## Action

Go up one layer of abstraction. Produce a map. Plain English. No deep code dive. No file dumps. No line-by-line.

## Output format

```
<module-A> — <one-line job>
  in:  <who calls it>
  out: <what it calls>
  seam: <interface boundary, if any>

<module-B> — <one-line job>
  in:  ...
  out: ...

<module-C> — ...
```

After the map, list the 1-3 most likely places relevant to the user's current task.

## Stop after the map

Wait for user direction on which thread to pull. Do NOT auto-dive.

## Example

```
auth/session.ts          — issues + validates session tokens
  in:  auth/login.ts, middleware/protect.ts
  out: db/users.ts, lib/jwt.ts
  seam: SessionStore interface (test seam, in-memory + redis adapters)

auth/login.ts            — handles email+password login flow
  in:  routes/auth.ts
  out: auth/session.ts, db/users.ts

middleware/protect.ts    — gate for authenticated routes
  in:  most route files
  out: auth/session.ts

Most likely relevant: auth/session.ts (token logic) and middleware/protect.ts (gate logic). Pick one.
```
