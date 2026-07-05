# craft-skills

A small set of installable agent skills that preserve and build the *human's* software-craft skill while working with AI, with the craft curriculum as the skills' internal reference material.

## Language

### The product

**Skill**:
An installable, self-contained directory (SKILL.md plus assets) that a user or model invokes. The unit of value; everything else in the repo serves one.
_Avoid_: tool, module, workflow

**Concept**:
A named, source-attributed unit of craft knowledge from the software canon (e.g., Red→Green→Refactor, Expose Your Ignorance).
_Avoid_: rule, lesson, pattern (as a synonym)

**Concept file**:
The canonical ~20-line rendering of one concept inside `craft-coach/concepts/`: source citation, when it applies, the rule, the anti-pattern, and an agentic-era section.
_Avoid_: rules.md (the old repo's form)

**Agentic-era section**:
The required part of every concept file that reinterprets the concept for work where an agent writes most of the code — not just restates the book.

### The coaching contract

**Surfacing**:
Naming a concept or anti-pattern, with its source, at the moment it applies — and letting the human act. The AI surfaces; it does not silently apply.
_Avoid_: enforcing, correcting, coaching (as the verb for the act itself)

**Asymmetric binding**:
The contract's shape: the rules bind the human's practice; the AI is bound only to surface them.

**AI laundering**:
Letting AI fluency substitute for one's own understanding. The central failure mode the project exists to fight.

### Provenance

**Author-verified**:
Content the repo's author has personally checked against the primary source. The strongest provenance class.

**Web-sourced**:
Content grounded in a high-trust source fetched at write time, cited by URL. Acceptable; never from parametric recall.

**Unverified draft**:
Content carrying an explicit marker that no one has checked it against its source yet. Visible by rule — never silent.
_Avoid_: laundered content (that's the failure, not a class)

**Observed**:
The provenance class for date-stamped empirical claims about model behavior (the agentic-era sections). Honest only with the date attached; ages as models change.

### The coaching contract

**Craft home**:
The `~/.craft/` directory — one per person, holding every personal artifact (coaching contract, mission, practice log, learning records). Never committed to a repo.

**Coaching contract**:
The `~/.craft/COACHING.md` file listing which disciplines a person has adopted, is trying on, or has turned off. The signed half of asymmetric binding — surfacing runs on it. Personal; applies across all their repos.
_Avoid_: config, settings

**Team standard**:
An entry in a repo-committed `TEAM-STANDARDS.md`: a discipline the team holds for that codebase, surfaced for everyone with team framing. About the code, not anyone's practice — never a substitute for a coaching contract.

**Checkpoint**:
The deliberate mode of craft-coach: invoked by the human at a decision moment (before accepting a diff, before merging). The reliable mode; opportunistic surfacing is the bonus.

**Study concept**:
A career-timescale concept with no session-observable trigger; lives in craft-learn and is reached through study sessions, never surfaced from coding events.

### The repo's lifecycle

**Bucket ladder**:
The governance path an idea travels: a workspace-local in-progress note → promoted to `skills/` (README entry required) → or a workspace-local out-of-scope note. Replaces spec-driven ceremony; only promoted work is published.
_Avoid_: pipeline, OpenSpec change

### Practice and learning

**Kata**:
A small, repeatable deliberate-practice exercise in one of four formats: test-driven, pattern-recognition, reflective, or review.

**Review kata**:
A kata whose exercise is critiquing a realistic, subtly-flawed AI-generated diff. The practice form for the judging-output skill the agentic era demands.

**Mission**:
The learner's written *why* for investing in craft (`MISSION.md`). Selects what to learn next; replaces tier self-assessment.
_Avoid_: roadmap, tier

**Learning record**:
An ADR-style note of what the learner actually internalized, kept in the learner's workspace.
_Avoid_: activity tracking, digest
