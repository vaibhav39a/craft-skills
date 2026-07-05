# Information Hiding

Source: David Parnas's idea, taught in John Ousterhout, *A Philosophy of Software Design* (2018) — provenance: web-sourced (https://web.stanford.edu/~ouster/cgi-bin/cs190-spring16/lecture.php?topic=modularDesign, https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lecture.php?topic=modularDesign)

## When it applies

- An implementation detail is about to become something another module depends on
- The same design decision shows up in more than one module
- Code is being structured around the *order* operations happen rather than around functionality

## The rule

Each module encapsulates knowledge — a design decision — and its interface should not reflect that decision (much). That's what makes interfaces simple and implementations changeable without touching other classes. It applies within classes too, not just at module boundaries. When knowledge has leaked across modules, the fix is consolidation into one place — sometimes that means a *larger* class, which is fine; small-class dogma is not the goal.

## Anti-patterns

- **Information leakage** — implementation details exposed; other classes now depend on them, and one decision change fans out
- **Temporal decomposition** — structuring modules around execution order (read-then-parse-then-write), which smears one piece of knowledge across all the steps

## In the agentic era

Temporal decomposition is an agent's natural grain — prompts arrive as step sequences, and the generated modules mirror the steps, leaking the shared knowledge across all of them. And when knowledge has already leaked, an agent won't feel the friction a human would: it happily edits all five copies at once, hiding the leak's cost until the human maintains it alone. Ask of any generated boundary: what decision does this module hide? If the answer is "none, it's step two," name the leak.
