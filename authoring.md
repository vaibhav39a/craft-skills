# Authoring

How concepts and skills are written in this repo. This is the only meta-doc.

## Concept files

One concept per file, ~20 lines, five sections. **Every concept has exactly one home, owned by its consumer**: session-surfaceable concepts live in `skills/craft-coach/concepts/<group>/<slug>.md`; study concepts (career-timescale, no session trigger) live in `skills/craft-learn/concepts/`. Groups are canon clusters (currently `design/`, `ddd/`, `refactoring/`, `tdd/`, `apprenticeship/`); a new canon area gets a new group directory and its own index section. **Sync rule**: a new or renamed concept file requires a matching index row in its owner's SKILL.md, and the sweep (files ↔ rows, 1:1) runs before the commit.

```markdown
# <Concept Name>

Source: <Author>, *<Work>* — provenance: author-verified | web-sourced (<URL>) | UNVERIFIED DRAFT

## When it applies
<2–4 bullet moments, concrete enough that a model can pattern-match mid-session>

## The rule
<the discipline itself, 2–4 sentences or bullets>

## Anti-patterns
<named anti-patterns, bolded — names are what craft-coach surfaces>

## In the agentic era (observed YYYY-MM)
<required: how the concept changes when an agent writes most of the code — reinterpretation, not restatement>
```

### The citation rule

Every concept names a real source. **Katas are not exempt**: a kata adapted from a known exercise names its originator on a `source:` line (e.g. Osherove's String Calculator). Four provenance classes:

- **author-verified** — the author of this repo has checked the content against the primary source. A file graduates to this class only through a real study session: read against the sources, kata run where one exists, learning record written. The record is the evidence; the marker is the receipt.
- **web-sourced** — grounded in a high-trust page fetched at write time, cited by URL. Fetched, not remembered.
- **UNVERIFIED DRAFT** — nobody has checked it yet. The marker stays, visibly, until someone does.
- **observed (YYYY-MM)** — empirical claims about *model behavior*, date-stamped on the section heading. Every "In the agentic era" section carries this class: its claims are experience-based, will age as models change, and are honest only with a date attached. The revisit trigger: when a file graduates to author-verified through the study loop, its observed stamp gets re-checked in the same session — the two sweeps are one activity.

Never write quotes, page numbers, or chapter numbers from parametric recall. An honest "unverified" beats a plausible fabrication — laundered canon is the failure mode this repo exists to fight.

## Skills

Two invocation modes, and the choice is the design (vocabulary adapted, with thanks, from mattpocock/skills' `writing-great-skills`):

- **User-invoked** — the human types it. Zero ambient context cost; reliability is structural. Prefer this.
- **Model-invoked** — the agent reaches for it when the description matches the moment. The description line is loaded every turn: it is the entire ambient footprint, so write it like a trigger, not a summary.

Write skills as direct behavioral instruction, not requirements prose. Lean on **leading words** — terms the model already has strong priors for ("surface", "relentless", "kata", "refute") — so one sharp sentence does the work of a page. Target: a skill delivers its full value on first invocation. If a section doesn't change the model's behavior, cut it.

## The bucket ladder

`in-progress/<idea>.md` → promoted to `skills/<name>/` → or `out-of-scope/<idea>.md` with a one-paragraph reason.

Promotion is a PR-sized decision with one gate: **a README entry exists** (the pitch: problem moment, canon grounding, install line). Deprecation is a move back out of `skills/` with a dated note. No proposals, no design docs, no archive ceremony — if an idea needs a long-form argument, that argument *is* its `in-progress/` file.
