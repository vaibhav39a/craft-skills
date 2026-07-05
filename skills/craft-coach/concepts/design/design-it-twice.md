# Design It Twice

Source: John Ousterhout, *A Philosophy of Software Design* (2018), ch. 11 — provenance: web-sourced (https://web.stanford.edu/~ouster/cgi-bin/cs190-spring15/lecture.php?topic=complexity, https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lecture.php?topic=modularDesign; note: the author-controlled web treatment is brief — the book chapter is the canonical exposition and isn't freely fetchable)

## When it applies

- Code is about to be written from the first design that came to mind
- A module boundary, interface, or data model is being committed without an alternative ever existing
- A design decision feels obvious — which is precisely when the second sketch is cheapest insurance

## The rule

Don't implement your first idea. Make two designs — genuinely different, not a strawman and a favorite — and compare; the comparison surfaces complexity problems before they're embedded. Then it's a loop, not a one-shot ritual: pick one, write some code, watch for red flags, revise, and use code review as another design pass.

## Anti-patterns

- **First-idea commitment** — the initial design ships because nothing ever competed with it
- **Strawman second design** — an alternative constructed to lose, which buys the ritual without the insurance

## In the agentic era

Generation made this pattern nearly free: two radically different designs cost minutes of agent time, so there is no longer any economic excuse for first-idea commitment. The failure mode has moved instead — accepting the agent's first *plausible* draft, which arrives fluent and confident and therefore feels compared-against-alternatives when it never was. Before implementation starts on a nontrivial boundary, ask for the second, structurally different design and make the comparison explicit. The judgment exercised in choosing between them is the design skill the human keeps.
