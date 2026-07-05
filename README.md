# dev-skills

**As AI writes more of the code, the human's craft skill becomes the scarce resource — and the AI itself should be enlisted to build that skill rather than erode it.**

Most AI coding tools optimize for the AI doing more. These skills invert that: the rules bind *your* practice, and the AI is bound to **surface** the rule at the moment it applies — by name, with its source — and let you act. The failure mode they exist to fight is **AI laundering**: letting the AI's fluency substitute for your own understanding.

## The skills

### craft-coach — the pair-programming contract

*The agent quietly did your thinking for you, and you shipped it →* `craft-coach`.

Model-invoked. When a concept from the software-craft canon applies to what you and the agent are doing — code drafted with no failing test, a "refactor" that changes behavior, a diff in a language you can't read critically — it names the concept, cites the source, names the anti-pattern forming, and leaves the move to you. Sixteen concepts ship inside it, from Beck's green-bar patterns to Hoover & Oshineye's apprenticeship patterns, each with an **In the agentic era** section that rereads the canon for work where an agent types most of the lines.

```
cp -r skills/craft-coach ~/.claude/skills/
```

### craft-learn — mission-driven study of the canon

*You keep meaning to actually learn this stuff →* `craft-learn`.

User-invoked. Turns a directory into a standing learning workspace: your `MISSION.md` (why you're investing in craft) plus your learning records pick what to study next — zone of proximal development, not a curator's ladder. Sources are fetched and cited at read time; the skill's standing rule is *never trust your parametric knowledge*.

```
cp -r skills/craft-learn ~/.claude/skills/
```

### craft-practice — deliberate practice, including for the reviewing era

*You can do it with thought but not fluidly →* `craft-practice`.

User-invoked. Facilitates katas in four formats — test-driven, pattern-recognition, reflective, and **review**: critiquing a realistic, subtly-flawed AI-generated diff, because judging output is the skill the agentic era actually demands. The AI facilitates and never executes, scores, or grades; your practice history lives in your workspace.

```
cp -r skills/craft-practice ~/.claude/skills/
```

## No TDD skill — on purpose

This repo ships no skill for driving the red-green-refactor loop. Good ones already exist (e.g. [mattpocock/skills](https://github.com/mattpocock/skills) `tdd`); use one of those, and `craft-coach` rides along naming violations ("that's **Big-step green**") as they form. Duplicating a commodity skill would spend effort exactly where this repo's evaluation said not to. See [docs/adr/0001-no-tdd-skill-of-our-own.md](docs/adr/0001-no-tdd-skill-of-our-own.md).

## Repo layout

Ideas start in `in-progress/`, get promoted to `skills/` (a README entry is the promotion gate), or land in `out-of-scope/` with a reason. How concepts and skills are written — including the provenance rules that keep the canon un-laundered — is in [authoring.md](authoring.md). The repo's origin story is in [docs/evaluation.md](docs/evaluation.md) and [docs/improvement-plan.md](docs/improvement-plan.md).
