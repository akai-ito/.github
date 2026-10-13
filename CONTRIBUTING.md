# Contributing to Ito

Thank you for looking. Ito is early: the [map](https://github.com/akai-ito/.github/blob/main/map.md)
holds the design, and nothing is built yet.

## Issues

Open them in the repository they concern: bugs, questions and ideas are all welcome. Running
instances of Ito file issues too, from a fixed template.

## How we build

- **In slices.** Each slice ships the server and the app together and starts from a storyboard:
  what you see, what you feel, and what must never happen. The protocol is derived from it.
- **Integration tests through real boundaries**: the client API, the event stream, real storage.
  Unit tests only for genuinely tricky pure logic; a test that mirrors the code is noise.
- **Known edge cases become the specification.** When a capability is ported, its known edge
  cases become integration scenarios before its code is written.
- **Every commit leaves the READMEs and docs accurate.**

## TypeScript

ito-core and ito-capabilities share these conventions, and their lint configs enforce them: CI fails
on a violation.

- **Modern and functional.** Arrow functions only; an async generator, which can't be an arrow, is
  the one exception. Decisions are pure functions over plain data, and a thin shell does the I/O,
  built from factory functions that return objects of functions. No classes.
- **Immutable by default.** `const` only, `readonly` types, no mutation of shared data. Transform
  with `map`, `filter` and `reduce`, and use `for…of` only where effects must run in order.
- **Failures are values.** An expected failure returns a small `Result<Value, Failure>` with a typed
  code, and becomes an HTTP error at the edge. `throw` is for bugs.
- **Types say what things are.** `type`, never `interface`. States are discriminated unions,
  matched with exhaustive `switch` statements. Ids are branded (`TurnId`, `MessageId`), created
  once at the edge after validation. `undefined` rather than `null`, except where the wire format
  says `null`.
- **Names are full words.** `message`, never `msg`. Factories are `create…`, predicates `is…` or
  `has…`, conversions `to…`; constants are camelCase with their unit (`heartbeatMs`); generics are
  named for what they hold (`Result<Value, Failure>`).
- **Comments only for a why the code can't carry.** Names and types say what.
- **Organised by domain.** Folders are domains (`conversation`, `store`, `engine`, `http`); files
  are kebab-case with named exports only; imports use `#` subpaths (`#store/messages.ts`) and name
  the file that defines the thing, with no barrel files.
- **`async` and `await`.** No `.then` chains or callbacks; `AbortSignal` for timeouts and
  cancellation.
- **Dependencies earn their place.** Node built-ins first, and a new dependency states its reason in
  the pull request that adds it. Versions are pinned exactly, and Dependabot proposes updates weekly.
- **Tests run on Vitest**, through real boundaries.

## Commits

- [Conventional Commits](https://www.conventionalcommits.org/): `feat:`, `fix:`, `docs:` and so
  on, with a body that says why.
- No tool-attribution lines, such as a `Co-Authored-By:` trailer for an AI assistant or a
  "Generated with" footer.
- A commit-msg hook checks both before anything leaves your machine, and CI checks again. Turn the
  hook on once per clone:

  ```sh
  git config core.hooksPath .githooks
  ```
