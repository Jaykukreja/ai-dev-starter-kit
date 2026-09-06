# Project rules

Read at the start of every session. These apply to all work — writing code and
reviewing it.

## Scope

Never read, write, search or list anything inside: node_modules, .next, dist,
build, out, coverage, .git, .opencode, vendor, .venv, __pycache__, logs,
uploads, tmp, lock files (package-lock.json, yarn.lock, pnpm-lock.yaml), *.log,
*.min.js.

Use `git ls-files` to find source files. Never walk the filesystem.

## Types

- Use `type` not `interface` unless `interface` is genuinely required
- No `any` types anywhere

## Components

- Every component has proper JSDoc
- Default export name matches the file name (BasketClient.tsx exports
  `function BasketClient()`)
- No `console.log`
- No `!important` Tailwind classes

## Exports

- Every full function or component file has a default export, named to match
  the file
- Exceptions, do not flag: type-only files, Next.js API routes, config files,
  partial snippets in a merge request

## Tests

- Every test description starts with "should"
- Testing utilities imported from the setup file, not directly from
  @react-testing-library
- Every component test file ends with an accessibility test

## Null safety and fallbacks

- Check data exists before accessing nested properties. Optional chaining used
  consistently.
- No empty-string fallbacks for required values. Missing required data is an
  error condition, handled explicitly.
- `??` not `||` for defaults. Zero and false are valid values and `||` swallows
  them.

## Dead code

- No commented-out code. Git history exists.
- No TODO without a ticket reference:
  - `// TODO(TICKET-1234): description`
  - `// TODO(@owner, Sprint N): description`
  - `// TODO(Next PR - id): description`

## Magic numbers

No unexplained numeric literals. `total * 0.2` is `total * DEFAULT_TAX_RATE`.
`if (limit > 100)` is `if (limit > MAX_ITEMS_PER_PAGE)`. `setTimeout(cb, 300)`
is `setTimeout(cb, DEBOUNCE_DELAY)`.

## Component design

- One clear purpose per component. Split components managing unrelated concerns.
- Presentation separated from business logic. Dumb components take data through
  props, hold no state, call no APIs. Smart components manage state and call
  APIs, then pass data down.
- A component too large to understand without extensive scrolling needs
  splitting.

## State management

- Simplest tool that fits. Local state for most cases.
- Avoid multiple sequential state updates from one user action.
- Related state that always changes together is grouped.
- Side effects cleaned up. Timers, subscriptions and pending requests cancelled
  on unmount.

## Store

The store manages state and nothing else.

- Belongs: getters, setters, reading values, updating with new data, resetting.
- Does not belong: business logic, conditionals, API calls, transformations,
  error handling, retry logic, validation.
- Business logic goes in `services/`. Transformations go in `utils/`. State goes
  in `store/`.
- Store functions named for what they do to state: `addItem`, `removeItem`,
  `updateQuantity`, `clearCart`, `resetFilters`. Not `saveToServer`,
  `fetchFromAPI`, `syncWithBackend`.

## API and data handling

- Every error case handled. Users told when something failed, ideally able to
  retry.
- No silently swallowed errors. Catching, logging to console and carrying on
  hides real problems.
- Errors carry context.
- Race conditions considered where data can change mid-request.
- Loading and empty states exist.
- API calls have timeouts. AbortController or Promise.race. Hanging requests tie
  up resources.
- Users who end up in an unexpected state have a route back to a known path.

## Data flow

- Shared data lives in a common parent or context, not fetched twice.
- Validate assumptions about data shape. An API that usually returns a value
  does not always.

## Effects

- Every value referenced inside useEffect is in the dependency array, unless
  there is a stated reason.
- Avoid cascading effects where one state change triggers another which triggers
  another.
- Async calls in useEffect have cleanup functions.

## Status codes

- `400` failed input validation, with a clear message
- `401` missing or invalid credentials
- `403` user cannot access the resource
- `502` or `504` network failures. Timeouts handled distinctly.
- `500` internal processing failure or malformed data

Server logs capture full detail: request context, parameters, user info, stack
traces.

Client messages are user-friendly. Never expose internals, stack traces, server
paths, API keys or config.

When re-throwing, preserve the original error. Attach status codes and error
types.

## Backend security

- No secrets in code. Keys, tokens, connection strings and passwords come from
  environment variables.
- Every request input validated before use. Never trust `req.body`,
  `req.params`, `req.query`.
- Database queries never interpolate user input. Parameterised queries or the
  ORM's query builder.
- No user-controlled value reaches a query operator position. In Mongoose, an
  object where a string was expected is a NoSQL injection.
- Auth checked before the work happens, not after.
- Every route that writes or deletes requires authentication.
- Rate limiting on anything abusable: login, signup, password reset, search,
  file upload.
- Password fields, tokens and internal flags excluded from responses. Explicit
  field selection beats returning whole documents.
- Responses never leak internals: no stack traces, file paths, driver errors or
  raw database errors reaching the client.

## Backend reliability

- Every async route handler catches its errors. An unhandled rejection in
  Express does not reach the error middleware.
- Database calls have timeouts. A hanging query holds a connection open.
- Every index a hot query depends on exists. No filtering or sorting on
  unindexed fields.
- No `await` inside a loop where calls are independent. Use `Promise.all`. No
  N+1.
- Schemas set `required`, `unique` and defaults where the data demands it.
  Validation at schema level, not only in the route.
- Anything that must succeed or fail together uses a transaction.
- Logs carry request context: route, user id, correlation id.

## Error boundaries

- Error boundaries exist for catastrophic failures, so one failing component
  does not crash the app.
- Error messages are user-friendly. A new developer should understand what went
  wrong and what to do next.

## Consistency

- Implementation matches existing patterns in the codebase.
- One approach per problem. No mixed approaches to the same problem in the same
  file.
- Naming conventions consistent across files, components, functions, variables.
- Repeated structures extracted into shared abstractions. Do not repeat
  yourself. Keep it simple.

## Never

- Never rename existing variables, functions or files unless that is the task.
- Never edit or delete existing comments unless that is the task.
- Never reformat code you did not otherwise need to touch.
- Never delete anything that was not part of the request.
- Never claim something works if you did not run it.
- Never invent an API, package, config key or function. If unsure it exists,
  check or say you are unsure.
- Never `git push`, `git commit` or `git reset` unless the task is about git.

## When unsure

Ask. A question costs one message. A wrong assumption costs a day.