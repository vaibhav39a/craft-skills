# dev-skills

Installable agent skills that preserve and build the *human's* software-craft skill while working with AI. The skills are the product; the craft curriculum is their internal reference material. Vocabulary lives in `CONTEXT.md`; how things get written here lives in `authoring.md`.

## Repo conventions

- **Buckets**: ideas start in `.scratch/in-progress/` (one markdown file each), get promoted to `skills/`, or land in `.scratch/out-of-scope/` with a one-paragraph reason. Promotion requires a README entry — no README pitch, no promotion. All working documents (evaluations, improvement plans, buckets, tracker) live under the gitignored `.scratch/`; only the product is published.
- **Concepts**: every concept has exactly one home, owned by its consumer — session-surfaceable concepts in `skills/craft-coach/concepts/`, study concepts in `skills/craft-learn/concepts/`. Format, provenance, and the index sync rule are in `authoring.md`; follow them for every new or edited concept.
- **No tdd skill here by design** — see `docs/adr/0001-no-tdd-skill-of-our-own.md` before adding one.

## Agent skills

### Issue tracker

Issues live as local markdown files under `.scratch/<feature>/` in this repo; there is no remote tracker and PRs are not a triage surface. See `docs/agents/issue-tracker.md`.

### Triage labels

The five canonical triage roles use their default strings (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`). See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: one `CONTEXT.md` and `docs/adr/` at the repo root. See `docs/agents/domain.md`.
