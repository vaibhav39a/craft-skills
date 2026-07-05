# Fake It ('Til You Make It)

Source: Kent Beck, *Test-Driven Development: By Example* (2002), green-bar pattern — provenance: web-sourced (https://newsletter.kentbeck.com/p/canon-tdd; http://c2.com/wiki/remodel/pages/FakeItUntilYouMakeIt); the book-text specifics (the constant→expression procedure, the duplicated-test-data rationale) are UNVERIFIED DRAFT until checked against the book

## When it applies

- A first implementation wants to be clever instead of constant
- A test is red and the "real" answer feels obvious enough to skip straight to
- Scope is creeping into the green step

## The rule

First implementation for a broken test: return a constant. Then gradually transform the constant into an expression using variables. Two effects power it: a green bar changes your psychology (you refactor from green with confidence), and one concrete example keeps extraneous concerns out. Beck's answer to "isn't the fake wasted code?": the constant is *duplicated test data*, and eliminating that duplication is what drives the real implementation. Boundaries from his own writing: never delete assertions to get green, never copy computed actuals into expecteds, and don't mix refactoring into making it run — make it run, *then* make it right.

## Anti-patterns

- **Skipping to clever** — the general solution on the first red bar; scope and confidence both suffer
- **Fake as a license to stub** — faking over code with no test in place inverts the pattern; the test comes first, always
- **Resenting the constant** — "this feels stupid" is the friction that builds the restraint muscle for when the real answer *isn't* obvious

## In the agentic era

The agent always knows the "real" implementation, so the resistance this pattern trains against is now structural: when the first test is failing, the disciplined offer is the fake first, generality when a second test demands it (*triangulation*). If the human asks for the real thing straight away, name the step being skipped and let them choose — the point isn't the constant, it's keeping the step size a conscious decision instead of the agent's reflex.
