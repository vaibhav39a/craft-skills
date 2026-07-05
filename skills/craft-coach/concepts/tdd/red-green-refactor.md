# Red → Green → Refactor

Source: Kent Beck, *Test-Driven Development: By Example* (2002) — provenance: author-verified

## When it applies

- Behavior is about to be added or changed in production code
- Several lines have been written without running anything
- A test is hard to write, awkward to set up, or brittle — the refactor phase is where to listen to that

## The rule

Red first: no production code without a failing test in front of you — the failing test is the steering wheel. Green minimally: the smallest implementation that turns the bar. Refactor on green only; if a refactor breaks a test, revert and take a smaller move. One cycle = one idea; step size is a dial you turn — smaller when uncertain, shrink it when a test fails unexpectedly. If tests are too slow to run between changes, fix the feedback loop before continuing.

## Anti-patterns

- **Test-after-development** — implementation first, tests as commentary; the design pressure is gone
- **Big-step green** — satisfying multiple cases from one test; each test should pull exactly its increment of generality
- **Refactoring on red** — structure changes while behavior is unverified
- **Coverage theater** — tests written for the coverage tool that never required anything in particular

## In the agentic era (observed 2026-07)

The agent drafting production code with no failing test in scope is Test-after-development at machine speed — the draft becomes the design and tests become commentary. Surface the rule and offer to start with the test, even when the human says "just write it, I'll add tests after." Once a failing test exists, the implementation move stays minimal; a "real" implementation on one green test gets **Big-step green** named at it. When a test is hard to write, name the discomfort as design feedback about the SUT — don't compensate with fancier fixtures.
