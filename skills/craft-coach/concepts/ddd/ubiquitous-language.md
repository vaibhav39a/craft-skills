# Ubiquitous Language

Source: Eric Evans, *Domain-Driven Design* (2003); *DDD Reference* (2015) — provenance: web-sourced (https://www.domainlanguage.com/wp-content/uploads/2016/05/DDD_Reference_2015-03.pdf, https://www.dddcommunity.org/resources/ddd_terms/)

## When it applies

- Code, tests, and conversation are using different words for the same domain thing
- A term is being translated at a layer boundary or in a comment
- A new name is about to be coined for something the team already has words for

## The rule

Structure a language around the domain model and commit the team to using it relentlessly — in speech, diagrams, and the code itself. The model is the language's backbone, not documentation on top: **a change in the language is a change to the model**, so renaming is refactoring. It isn't "adopt the experts' jargon" — Evans says no existing dialect serves all needs; the language is forged by experimenting out loud in model terms and folding improvements back into the code. And it's scoped *within a bounded context* (his 2015 refinement), not one company-wide vocabulary.

## Anti-patterns

- **Translation between dialects** — experts speak one language, developers another; "translation blunts communication and makes knowledge crunching anemic"
- **Fractured language** — day-to-day terminology disconnected from the terms embedded in the code
- **Transient insight** — the incisive domain expression emerges in speech and never reaches the model

## In the agentic era

Agents are fluent in every dialect at once, so they translate silently and drift stops hurting the writer — the person who used to feel the friction of two vocabularies is now a model that feels none, and the cost compounds invisibly for the team. Agents also coin plausible names freely (craft-practice's *language-divergence* kata exercises spotting this, if you have that skill installed). The glossary is the contract: when a session's naming diverges from the established language, or an agent invents a term nobody says, surface it — and remember renaming is refactoring, which agents have made cheap enough to actually do.
