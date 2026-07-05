# Language Divergence

format: reflective
concept: ubiquitous-language
time-box: 30–45 min

## Setup

A real codebase you own or work in daily — not sample code. Pick one feature or user-facing capability you can narrate out loud ("a customer cancels their subscription").

## Goal

A written inventory of every place the code's language diverges from how you and your team actually *talk* about that capability, and a judgment about each divergence: harmless drift, or a hidden boundary?

## Rules of engagement

- Narrate the capability out loud (or in writing) in domain terms first, before opening the code. That narration is your reference vocabulary.
- Then walk the feature's path through the code — entry point to persistence — and record every mismatch: synonyms (`Client` vs the `Customer` you said), translations at layer boundaries, overloaded terms (one `Order` class serving two meanings), code-only jargon no one says in conversation.
- Record, don't refactor. This kata produces observations, not commits.

## Steps

1. Write the two-paragraph domain narration.
2. Trace the code path; keep a two-column log — *what the code says* / *what we say*.
3. For each divergence, note who translates (which layer, which person, which comment) and what that translation costs.
4. Classify each: drift (one vocabulary should win), or boundary (two contexts genuinely speak differently — see *bounded-context*).

## Variations

1. **Newest feature** — where language should be freshest; drift here is a process signal.
2. **Oldest module** — archaeology; which terms died in conversation but live in code?
3. **Agent-built feature** — trace a capability an agent implemented; log which vocabulary it picked and where it invented terms nobody uses.
4. **Cross-team seam** — trace a path that crosses another team's code; divergences here are candidate context boundaries, not bugs.

## Reflection prompt

One paragraph: which single renaming would pay for itself fastest, and which divergence turned out to be a boundary you should *stop* trying to unify?
