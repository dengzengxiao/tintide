# AGENTS.md

This file is the working contract for AI agents and human contributors in the
Tintide repository. It applies to the whole repository unless a deeper
`AGENTS.md` is added later.

## Project context

Tintide is an early-stage, time-aware color scheme generator. The MVP is one
hand-designed, Everforest-inspired theme with a semantic base palette, 24 solar
term keyframes, daily solar-event keyframes, smooth transitions, and a CLI.
The repository may be empty when implementation begins.

Read `README.md` and `ROADMAP.md` before making implementation decisions.

## Current scope

The first implementation task is the smallest vertical slice:

1. initialize the project;
2. define semantic palette types;
3. add one hard-coded built-in palette as data;
4. implement `tintide palette` with human-readable and JSON output;
5. add focused tests.

Do not implement GUI, a background daemon, automatic geolocation, desktop
integration, or multiple built-in themes until the MVP scope explicitly calls
for them.

## Architecture rules

- Keep time, color math, interpolation, and validation in a reusable core.
- Keep CLI parsing and terminal formatting at the application boundary.
- Keep the core deterministic and free of filesystem, network, and terminal I/O.
- Use semantic roles (`background`, `foreground`, `red`, `success`, etc.), not
  application-specific names or scattered hex literals.
- Store theme data separately from algorithms where practical.
- Keep adapters (Base16, terminals, editors, desktop environments) outside the
  core and make them consume semantic colors.
- Prefer the simplest correct design over speculative abstractions.

## Color rules

- Use OKLCH for user-facing color configuration and OKLab or OKLCH for
  interpolation.
- Do not hand-write standard color conversion matrices when a maintained,
  suitable library exists.
- Handle hue wrapping through the shortest path and define behavior when chroma
  is near zero.
- Convert to the target color space before gamut and contrast checks.
- Do not clip RGB channels independently as a gamut-mapping strategy; reduce
  chroma or use a documented mapping algorithm.
- Preserve semantic meaning: error colors must remain errors as time changes.
- Keep text/background contrast configurable and test it. Do not claim medical
  eye-care benefits.
- Keep annual and daily cycles continuous at their boundaries, including the
  end/start of the year.

## Implementation workflow

For every change:

1. inspect the relevant files and state assumptions;
2. describe the smallest change and its acceptance criteria;
3. implement only that change;
4. format, compile, lint, and test using the project toolchain;
5. inspect `git diff` and report files changed, tests run, and remaining risks.

AI agents must not silently expand the task, add dependencies, rewrite unrelated
files, or claim a command works without running it. If a dependency is needed,
explain why, its license, and why an existing dependency is insufficient.

## Testing expectations

Color and time logic needs tests for:

- round-trip conversion within documented tolerance;
- interpolation endpoints and hue wrapping;
- low-chroma behavior;
- gamut mapping;
- contrast validation;
- invalid configuration and boundary values;
- daily and annual cycle continuity;
- deterministic output for identical inputs.

Tests should be focused and readable. Add sampled full-year tests when the
implementation reaches real seasonal and solar-time calculations.

## Beginner-friendly collaboration

The project owner is learning software development and uses AI as a coding
assistant. Explain new types, dependencies, and non-obvious math in plain
language. After each meaningful change, summarize the data flow and invite
inspection of the diff. Never hide generated code behind large unrequested
refactors.

The owner makes the final decisions about visual quality, product scope, and
whether a generated result is acceptable. The agent is responsible for making
those decisions testable and for clearly identifying uncertainty.

## Documentation and language

Keep user-facing documentation available in English (en-US) and Simplified
Chinese (zh-CN). Code identifiers, CLI flags, and serialized field names stay
in English for consistency. Comments should be concise and explain intent or
non-obvious constraints, not restate code.

## Git and safety

- Preserve existing user changes.
- Do not use destructive commands such as `git reset --hard` or `git checkout`
  to discard work.
- Keep commits small and coherent when the owner asks for commits.
- Do not commit secrets, credentials, generated caches, or machine-specific
  paths.
