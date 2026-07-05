# Two Hats

Source: Kent Beck's metaphor, passed on in Martin Fowler, *Refactoring* (2nd ed., 2018) — provenance: web-sourced (https://martinfowler.com/articles/preparatory-refactoring-example.html, https://martinfowler.com/articles/workflowsOfRefactoring/fallback.html)

## When it applies

- A behavior change and a structural cleanup are happening in the same move
- A "refactor" is quietly changing what the code does
- A bug fix is sprouting opportunistic tidying

## The rule

At any moment you wear one hat. The hats are distinguished by *rules about test state*, not just intent: under the refactoring hat, every change is small and behavior-preserving, you work on green, and a failing test means you made a mistake; under the adding-function hat, new tests appear and red bars are expected. Swap hats as often as every couple of minutes — but deliberately, and only one at a time. Fowler's operational rhythm: refactor first to make the change easy, then make the easy change.

## Anti-patterns

- **Mixed-hat change** — feature and cleanup in one diff; when a test breaks, you can't tell which force broke it
- **Behavior change disguised as refactoring** — the most dangerous mix, because review reads it as safe
- **Opportunistic cleanup mid-fix** — the human version: "while I'm here…" inside a bug fix

## In the agentic era

Agents mix hats by default: asked to add a feature, they also "improve" the surrounding code — a silent behavior change wearing a cleanup's clothes, at a diff size that discourages careful review. When drafting, keep the hats in separate changes: complete the behavior change before touching structure, or refactor first with no behavior change at all. When a mixed-hat draft appears, name it and offer the split.
