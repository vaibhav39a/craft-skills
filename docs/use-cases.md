# When to use these skills

*A guide for a reader with no prior context. It assumes one thing about you: an AI agent now writes a meaningful share of your code, and you've noticed that this changes what your own skill is for.*

## The three skills in one paragraph each

**craft-coach** coaches against a contract **you** write — a `COACHING.md` listing which disciplines you've adopted, which you're trying on, and which are off. No contract, no nagging. It runs two ways: **invoke it deliberately as a checkpoint** (before accepting a nontrivial diff, before merging, at session end — the reliable mode), and let it fire opportunistically mid-session when something from the software-craft canon ("the canon" = the classic books: Beck, Fowler, Evans, Ousterhout, and company) matches what's happening — a "refactor" that quietly changes behavior, generated code sprouting speculative options nobody asked for. Either way it names the concept, cites the source, names the anti-pattern, and leaves the decision to you.

**craft-learn** turns any directory into a standing study workspace. You write a `MISSION.md` (*why* you're investing in craft); sessions then pick what to study next based on that mission and what your learning records show you've already internalized. It fetches and cites real sources at read time — it never teaches from the model's memory of a book.

**craft-practice** runs deliberate-practice katas in four formats — test-driven, pattern-recognition, reflective, and **review** (critique a realistic, subtly-flawed diff, then see what you missed). It facilitates and never solves, scores, or grades. Your practice history lives in a `PRACTICE.md` in your workspace.

They compose but install independently. If you install only one, start with the one your section below points at.

## Getting set up

Install a skill by copying it into your assistant's skills directory — e.g. `cp -r skills/craft-coach ~/.claude/skills/` (same for the other two; install them side by side, they find each other as siblings). User-invoked skills are run by asking for them — in Claude Code, type `/craft-learn` or `/craft-practice`; craft-coach can be invoked the same way for a checkpoint. To update later: delete the installed copy and re-copy (see the README's update note).

**Where your files live** — one rule: everything personal goes in **`~/.craft/`**, your craft home, shared by all three skills and never committed to any repo:

```
~/.craft/
├── COACHING.md          ← your personal coaching contract (craft-coach)
├── MISSION.md           ← why you're investing in craft (craft-learn)
├── RESOURCES.md         ← your growing, cited reading list (craft-learn)
├── learning-records/    ← what you've actually internalized (craft-learn)
├── PRACTICE.md          ← your kata log (craft-practice)
└── scratch/             ← throwaway kata code
```

The only repo-committed artifact is `TEAM-STANDARDS.md` — a team's standards for a codebase, distinct from anyone's personal contract (see the senior section).

---

## Junior: the skills you're supposed to be building

The risk at this stage is specific: the agent's output is better than what you'd write alone, so it's easy to ship months of code you couldn't have written and can't fully judge. That gap doesn't announce itself — it shows up later, in the debugging session where the agent's context is gone and yours never existed.

**"I just shipped agent code I don't really understand."**
This is craft-coach's central use case — it names the moment (*AI laundering*, from *expose-your-ignorance*, the concept the whole system is built around) as it happens, not in retrospect. Install it, and when you've accepted several suggestions in a row without a question, it will ask you to walk back through the last change. Saying "explain it again, simpler" to your agent is the modern form of the oldest apprenticeship pattern.

**"I want to actually learn fundamentals, not just prompt better."**
Start craft-learn with an honest mission — e.g. *"I review more agent code than I write; I want the judgment to catch what it gets wrong."* The mission picks your syllabus; sessions start by quizzing what you studied last (retrieval beats rereading). The career-stage concepts — *your-first-language* (depth in one language beats fluency-by-proxy in ten), *concrete-skills* (what can you do *without* the agent?), *sweep-the-floor* (how to earn trust on a first team) — live here as study material.

**"I want to try TDD without pretending I've mastered it."**
Save a copy of `COACHING-template.md` as `~/.craft/COACHING.md` and put *red-green-refactor* under **Trying on** — the coach will surface it gently, once a session, instead of policing you, in every repo you work in. Run the string-calculator kata (craft-practice) to get the cycle into your hands before using it on real work.

*Start with:* craft-learn (with a real mission) + the review kata in craft-practice, which trains the one skill this era demands of juniors most: judging a diff you didn't write.

## Mid-level: the skills that are quietly atrophying

You can build features fine. The mid-level risks are subtler: your output volume has tripled but your *design* decisions are increasingly the agent's defaults, and your codebase understanding is increasingly secondhand.

**"Every 'simple' change seems to touch six files now."**
That's *change amplification* — one of Ousterhout's three complexity symptoms, and craft-coach will name it when it sees it. The design track (deep-modules, information-hiding, pull-complexity-downwards) exists because agents amplify design defaults: many small pass-through classes, config decisions punted to callers, error handling everywhere. Someone has to hold the design line, and the agent won't.

**"I'm about to build on a nontrivial boundary."**
*design-it-twice*: generation made a second, structurally different design nearly free — the only remaining failure mode is accepting the first plausible draft. Ask for two; choosing between them is the design skill you keep.

**"I've inherited legacy code and the agent wants to 'improve' it."**
The tdd group's legacy pair: *characterization-tests* (pin what the code actually does before anyone — human or agent — changes it) and *listen-to-the-tests* (when a test is hard to write, the design is talking; an agent will build the mock network a human would have refused to type, and the signal dies in the fixture).

**"My team says 'customer' in meetings and the code says `client`, `account`, and `user`."**
The ddd group: *ubiquitous-language* and *bounded-context*. Run craft-practice's language-divergence kata on your own codebase — narrate a feature in domain terms, trace the code, log every mismatch, and classify each as drift or a hidden boundary.

*Start with:* craft-coach with a real COACHING.md, plus the module-depth and smell-spotting katas — pattern-recognition for the structural reading that cosmetically-clean agent output defeats.

## Senior: the skills the role now runs on

At this level you write the least code and sign off on the most. Review capacity is your bottleneck, other people's judgment is your multiplier, and the strategic calls — boundaries, integrations, what *not* to build — are the ones no agent can own.

**"I review far more than I write, and green CI tells me nothing."**
The review-format katas are calibration training: each canned kata ships a realistic diff where CI is green and a handful of flaws hide in plain sight, with the answer key in a separate file nobody opens until the critiques are written. Run one yourself; then run it with your team using the kata's "Running this with a team" flow — everyone critiques independently, then the key comes out and you compare. It makes review judgment discussable instead of tacit.

**"Agents are integrating our systems faster than we're deciding how they should relate."**
The strategic-DDD concepts: *context-mapping* (an integration drafted against an upstream API quietly conforms to its model — a relationship chosen by no one), *aggregates* (generated CRUD is a reference free-for-all; consistency boundaries appear in no diff because no test demands them), *bounded-context* (boundaries an agent will respect must be declared, not sensed). The strategic call is yours; the translation code is the agent's.

**"Half of every generated PR is capability nobody asked for."**
*yagni* is arguably the canon's highest-frequency surfacing moment now: cost of build collapsed, cost of carry didn't. A senior who names *the presumptive feature* consistently changes what their whole team ships.

**"My own hands are getting slow."**
Steering agents all day atrophies exactly the fluency your judgment rests on. A 20-minute kata cadence (craft-practice tracks rotation so repetition stays varied) and *reflect-as-you-work* — which craft-coach surfaces when a meaningful task closes unexamined — are the maintenance plan. *record-what-you-learn* turns your hard-won calls into material your team can study.

*Start with:* the canned review kata as a team exercise, and two distinct files: your personal `~/.craft/COACHING.md`, and a committed `TEAM-STANDARDS.md` in the repo — the team's standards for the codebase, surfaced for everyone with team framing. They are deliberately not the same artifact: standards are about the code; a coaching contract is a personal signature, and nobody else should inherit yours (see ADR-0003).

---

## One honest caveat

These skills surface and facilitate; they don't measure. Whether the coaching actually fires at the right moments in *your* sessions is something you'll observe, not something we can promise. If a surfacing was apt or noise, note it; the contract file is yours to tighten.
