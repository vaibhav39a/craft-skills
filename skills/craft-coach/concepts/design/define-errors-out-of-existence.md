# Define Errors Out of Existence

Source: John Ousterhout, *A Philosophy of Software Design* (2018) — provenance: web-sourced (https://web.stanford.edu/~ouster/cgi-bin/cs190-spring16/lecture.php?topic=exceptions, https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lecture.php?topic=exceptions, https://web.stanford.edu/~ouster/cs190-winter23/lectures/aposd)

## When it applies

- Error handling is spreading across callers instead of the API changing
- An exception is about to be thrown with no clear picture of how the caller would handle it
- A "suspicious-looking" input is about to be rejected defensively

## The rule

Exceptions are a major source of complexity, so reduce the number of places that must handle them. Four techniques, strongest first: **define the error out of existence** by changing API semantics so the case can't occur (unsetting a nonexistent variable just succeeds; substring clamps its bounds); **mask** it (recover automatically, report nothing); **aggregate** (one handler for many cases, promoted or deferred to where a handler already exists); **crash** when no viable handling exists. Before throwing, ask how the caller will handle it — if unclear, consider a return value. Ousterhout's own caution: use the idea judiciously; it's easy to take too far.

## Anti-patterns

- **Defensive programming** — throwing for anything suspicious-looking; every throw taxes every caller
- **Punting** — surfacing the problem instead of solving it, which is complexity pushed to whoever calls you

## In the agentic era (observed 2026-07)

Defensive programming is the agent default: generated code arrives wrapped in try/except and studded with validation throws, because locally that always *looks* responsible. Each one is a caller obligation nobody designed. When agent output multiplies error paths, surface the stronger move — can the API's semantics make the case impossible, or one aggregation point absorb it? The design question ("who handles this, and should anyone have to?") is exactly what generation skips.
