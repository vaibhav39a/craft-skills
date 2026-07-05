# Code Smells

Source: term coined by Kent Beck; catalog in Fowler & Beck, *Refactoring* (1999, 2nd ed. 2018), ch. 3 — provenance: web-sourced (https://martinfowler.com/bliki/CodeSmell.html)

## When it applies

- Something in the code catches the eye — too long, too many parameters, data traveling in packs
- A review is about to wave code through because it's syntactically clean
- A "fix every warning" pass is about to treat indicators as defects

## The rule

A smell is "a surface indication that usually corresponds to a deeper problem" — and both halves matter. *Surface*: it must be sniffable, quick to spot without deep analysis. *Usually*: smells don't always indicate a problem — some long methods are legitimate. The smell buys you an investigation, not a refactoring: look deeper, find whether a real problem sits underneath, then decide. The skill being trained is the mapping from signal to underlying design question, not memorizing the catalog.

## Anti-patterns

- **Smell-blindness** — reading only for correctness and style, so the structural signals pass review
- **Reflex-fixing** — treating every smell as a defect to eliminate on sight; you destroy the signal's information and sometimes "fix" legitimate code
- **Catalog worship** — naming the smell and stopping, as if the label were the diagnosis

## In the agentic era (observed 2026-07)

Agent output is cosmetically immaculate — well-named, well-formatted, comment-tidy — which defeats the eye's usual triggers; the smells that survive generation are structural (feature envy across generated classes, data clumps in generated signatures), so the sniffing must happen at the design level, exactly where human review is scarcest. And agents will happily reflex-fix: asked to "clean up smells," they'll refactor everything that pattern-matches, including the legitimate long method. Keep the human in the *usually* — surface the smell, name the deeper question it raises, and let the human decide whether it's disease or just odor.
