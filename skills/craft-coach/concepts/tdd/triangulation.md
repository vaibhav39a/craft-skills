# Triangulation

Source: Kent Beck, *Test-Driven Development: By Example* (2002), "Triangulate" green-bar pattern — provenance: web-sourced (https://www2.cs.uh.edu/~rsingh/documents/software_design/TDD.pdf, Beck's primary text, university-hosted)

## When it applies

- One green test is about to justify a general implementation
- The right abstraction for a calculation is genuinely unclear
- A faked constant is ready to become real code

## The rule

Only abstract when you have two or more examples. One assertion can be satisfied honestly by a constant; the second test — with argument values chosen so no shortcut survives — is what pulls the real generality out of the code. Beck's own caveat, usually lost in retelling: he reaches for triangulation only when *really unsure* about the abstraction; otherwise Obvious Implementation or Fake It. It's a move for uncertain territory, not a universal rule — and taken literally its rules loop forever (once the abstraction exists, the second assertion is redundant again).

## Anti-patterns

- **Generalizing from one example** — the abstraction is a guess wearing a green bar
- **Over-triangulation** — two tests before every generalization, even when the pattern is obvious; Obvious Implementation is the escape hatch
- **A second test the fake also passes** — argument values too similar to force anything

## In the agentic era

Agents produce the general solution from the first test, every time — generality is their reflex, and one green test makes it look earned. Triangulation is the discipline that says *not yet*: when an implementation is about to satisfy cases no test demands, surface it and offer the triangulating second test instead. The human's judgment call — is this territory uncertain enough to triangulate? — is exactly the judgment the reflex would erase.
