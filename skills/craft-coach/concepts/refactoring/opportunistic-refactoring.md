# Opportunistic Refactoring

Source: Martin Fowler — provenance: web-sourced (https://martinfowler.com/bliki/OpportunisticRefactoring.html)

## When it applies

- You're passing through code and see a quick improvement
- Refactoring is being deferred to a someday "cleanup sprint"
- A small mess is about to be stepped over for the third time

## The rule

Codebase health comes from a continuous stream of small improvements made "whenever and wherever code needs to be cleaned up — by whoever," as part of whatever task you're doing — not from scheduled refactoring phases. Fowler's page calls it the **camp site rule**: always leave the code behind in a better state than you found it. The discipline boundary is explicit: only refactor on green tests. Fowler also names the honest frictions: weak test coverage demands extra caution, feature branches discourage it (merge pain), and strong code ownership creates friction.

## Anti-patterns

- **Cleanup sprint someday** — health deferred to a phase that's always next quarter
- **The rabbit hole** — Fowler's own warning: "as you fix one thing you spot another"; opportunistic means quick and bounded, not spelunking
- **Camping on red** — improving structure while tests fail, which is *two-hats* mixed

## In the agentic era

This one cuts both ways. Agents make the camp site rule nearly free — the small rename, the extracted function, done in seconds on green tests. But the agent version of "while I'm here" is also the classic mixed-hat diff: unsolicited improvements bundled into feature changes, silently. And the rabbit hole is bottomless for a tireless fixer — an agent will follow "you fix one thing, you spot another" forever. The frame: opportunistic refactoring is welcome as *separate, small, green-to-green* changes the human sees and approves; inside a feature diff, name the hat-mixing and offer to split it out.
