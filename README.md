# dev-skills

**As AI writes more of the code, the human's craft skill becomes the scarce resource — and the AI itself should be enlisted to build that skill rather than erode it.**

Most AI coding tools optimize for the AI doing more. These skills invert that: the rules bind *your* practice, and the AI is bound to **surface** the rule at the moment it applies — by name, with its source — and let you act. The failure mode they exist to fight is **AI laundering**: letting the AI's fluency substitute for your own understanding.

New here? [docs/use-cases.md](docs/use-cases.md) maps concrete scenarios — junior, mid-level, senior — to the skill and concept that serves each, and shows where your files live.

## The skills

### craft-coach — the pair-programming contract

*The agent quietly did your thinking for you, and you shipped it →* `craft-coach`.

Runs two ways: invoke it deliberately as a **checkpoint** (before accepting a nontrivial diff, before merging), or let it fire opportunistically when a concept from the software-craft canon matches what you and the agent are doing — a scaffold sprouting shallow classes, a "refactor" that changes behavior, a first design going straight to implementation. Either way it names the concept, cites the source, names the anti-pattern forming, and leaves the move to you.

Coaching runs on consent, never on defaults you didn't sign: your personal contract lives at `~/.craft/COACHING.md` (adopted / trying-on / off — TDD cycle mechanics fire only if adopted; `spike:` lines mark throwaway work as off-limits), and a repo-committed `TEAM-STANDARDS.md` carries a *team's* standards for a codebase with separate semantics ([ADR-0002](docs/adr/0002-coaching-consent-artifact.md), [ADR-0003](docs/adr/0003-team-standards-vs-personal-contract.md)). Templates for both ship with the skill.

The curriculum ships inside it across five canon groups — Ousterhout's deep modules and complexity symptoms, Evans's ubiquitous language and bounded contexts, Fowler's code smells and YAGNI, Beck's green-bar patterns, the session-observable apprenticeship patterns — each concept ~20 lines with a named anti-pattern, an honest provenance line, and an **In the agentic era** section (date-stamped: claims about model behavior age) that rereads the canon for work where an agent types most of the lines.

```
cp -r skills/craft-coach ~/.claude/skills/
```

### craft-learn — mission-driven study of the canon

*You keep meaning to actually learn this stuff →* `craft-learn`.

User-invoked (`/craft-learn`). Your standing study workspace lives at `~/.craft/`: a `MISSION.md` (why you're investing in craft) plus your learning records pick what to study next — zone of proximal development, not a curator's ladder; sessions open with retrieval practice, not rereading. Sources are fetched and cited at read time; the skill's standing rule is *never trust your parametric knowledge*. It ships the career-timescale study concepts (sweep-the-floor, concrete-skills, be-the-worst, your-first-language) and a curated reading list as seed material.

```
cp -r skills/craft-learn ~/.claude/skills/
```

### craft-practice — deliberate practice, including for the reviewing era

*You can do it with thought but not fluidly →* `craft-practice`.

User-invoked (`/craft-practice`). Facilitates katas in four formats — test-driven, pattern-recognition, reflective, and **review**: critiquing a realistic, subtly-flawed diff, because judging output is the skill the agentic era actually demands. Nine katas ship, from Osherove's string calculator (with green-bar-move variations) through characterization and test-pain diagnosis to two hand-authored review katas — with **answer keys and sample banks kept in separate files** nobody opens until the critique is written, and a "Running this with a team" flow for calibration exercises. The AI facilitates and never solves; comparing against an authored key is calibration, judging you is off the table. Your practice log lives at `~/.craft/PRACTICE.md`.

```
cp -r skills/craft-practice ~/.claude/skills/
```

## Installing and updating

Install skills side by side under one skills directory (they resolve each other as siblings): `cp -r skills/craft-<name> ~/.claude/skills/`. To **update**: delete the installed copy first, then re-copy — `cp -r` alone won't remove files a new version dropped. Check what you're running against the `version:` line in each installed SKILL.md. If you used this project's predecessor repo, uninstall its skills (`dev-skills-practice`, `dev-skills-scaffold`, `craft-tdd`) — they answer to the same trigger words with outdated behavior. Your personal files live in `~/.craft/` and survive every reinstall.

## Repo layout

The product is `skills/`; promotion into it requires an entry in this README. How concepts and skills are written — the concept-file format, the four provenance classes that keep the canon un-laundered, the index sync rule — is in [docs/authoring.md](docs/authoring.md). Architectural decisions are recorded in [docs/adr/](docs/adr/); the project vocabulary is in [CONTEXT.md](CONTEXT.md). One deliberate absence: no TDD-loop skill ships here — `craft-coach` surfaces cycle violations while any tdd skill drives ([ADR-0001](docs/adr/0001-no-tdd-skill-of-our-own.md)). MIT licensed.
