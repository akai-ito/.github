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
