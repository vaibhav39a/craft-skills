# Pull Complexity Downwards

Source: John Ousterhout, *A Philosophy of Software Design* (2018) — provenance: web-sourced (https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lecture.php?topic=modularDesign, https://web.stanford.edu/~ouster/cgi-bin/cs190-spring15/lecture.php?topic=complexity)

## When it applies

- A module is about to expose a configuration parameter instead of picking a sensible behavior
- An error is about to be thrown upward instead of handled where it arose
- "Simple implementation" is winning an argument against "simple interface"

## The rule

The module author embraces the suffering: take on the hard problem, solve it completely, make the solution easy for others — let a few module developers hurt rather than thousands of callers. Ousterhout's lecture name for it: the **Martyr Principle** — take more pain yourself so others have less. The two flagship applications: handle error conditions rather than throwing them (see *define-errors-out-of-existence*), and minimize configuration parameters, each of which is complexity punted upward to a user who knows less than you about the right value.

## Anti-patterns

- **Punting upward** — exceptions and config knobs as a substitute for making a decision; locally easier, globally more expensive
- **Simple-implementation bias** — optimizing for the module author's afternoon over every caller's future

## In the agentic era (observed 2026-07)

Agents punt upward reflexively — a config parameter or a thrown exception is always the locally simplest thing to generate, and the cost lands on future callers the agent will never meet. The economics have flipped in your favor though: when the *agent* is the martyr, pulling complexity down is cheap — but only if the human demands it. When a generated interface asks its caller to decide something the module should own, name the punt and ask for the version that suffers so callers don't.
