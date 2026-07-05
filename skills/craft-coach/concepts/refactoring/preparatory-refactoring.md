# Preparatory Refactoring

Source: workflow named by Martin Fowler; the slogan is Kent Beck's — provenance: web-sourced (https://martinfowler.com/articles/preparatory-refactoring-example.html, https://martinfowler.com/bliki/OpportunisticRefactoring.html)

## When it applies

- An upcoming change is awkward to make in the code as it stands
- A feature is about to be forced through a structure that resists it
- The estimate for a "simple" change keeps growing because of where it has to land

## The rule

Beck's formulation: **make the change easy, then make the easy change** — first refactor into the structure that makes the feature trivial, then add it. The payoff is risk, not just convenience: refactoring mode is the safe mode (behavior-preserving, tests green), so front-loading the structural work keeps the time spent in risky feature-addition mode short. Jessica Kerr's metaphor, which Fowler borrows: don't traipse due east through the woods — go twenty miles north to the highway and cover the distance at three times the speed. The detour *is* the quickest route.

## Anti-patterns

- **Brute-forcing the woods** — wedging the feature into hostile structure because refactoring first "takes too long"
- **Preparation that never ends** — the detour becoming a rewrite; preparatory refactoring is scoped by the change it serves

## In the agentic era

Agents brute-force the woods by default: give one a feature request and it will thread the awkward structure heroically, shims and special cases included, because nothing in generation feels the resistance a human would. The question to ask before implementation — *would this be easy if the structure were different?* — costs one prompt now, and the refactoring leg is exactly the safe, test-guarded work agents execute well. When a draft is visibly fighting the existing structure, name the missing preparation step and offer the two-move sequence instead of the wedge.
