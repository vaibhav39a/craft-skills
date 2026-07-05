# Self-Testing Code

Source: Martin Fowler, *Refactoring* (2nd ed., 2018); also foundational in Michael Feathers, *Working Effectively with Legacy Code* (2004) — provenance: web-sourced (https://martinfowler.com/bliki/SelfTestingCode.html)

## When it applies

- A change is about to land somewhere no test would catch its breakage
- Refactoring is proposed on code without a test net
- Tests exist but nobody knows whether they'd actually fail if behavior changed

## The rule

Self-testing code is a *property*, not a technique: you can run the suite and be confident that if it passes, the code is free of substantial defects. Fowler decouples it from TDD — TDD is one practice that produces it; test-after can too. The outcome is the concept. The benefit is chiefly psychological: confidence to change the system, which is what makes refactoring possible instead of fear-driven stagnation. Verify the property by sabotage: deliberately break a behavior and watch a test fail. If nothing fails, the code isn't self-testing — whatever the coverage number says.

## Anti-patterns

- **Tests that can't fail** — happy-path assertions that pass even when the code is broken
- **Coverage as the property** — coverage is a proxy; behavior-change detection is the actual thing
- **Refactoring without the net** — without tests that fail on behavior change, "refactoring" is gambling

## In the agentic era (observed 2026-07)

An agent's refactoring draft in untested code is gambling at machine speed — the diff looks plausible, and plausible is exactly what an unverified behavior change looks like. Before accepting agent changes, ask whether a test would catch this breaking; if not, surface that the precondition is missing and that *characterization tests* are how to establish it on legacy code.
