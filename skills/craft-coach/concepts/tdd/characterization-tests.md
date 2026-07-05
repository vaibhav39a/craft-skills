# Characterization Tests

Source: Michael Feathers, *Working Effectively with Legacy Code* (2004) — provenance: web-sourced (http://c2.com/wiki/remodel/pages/CharacterizationTest, https://www.artima.com/weblogs/viewpost.jsp?thread=198296)

## When it applies

- Untested or undocumented code is about to be changed
- Behavior needs learning on a codebase nobody fully understands — where the "correct" behavior may be unknowable and actual behavior is the only baseline

## The rule

Lock in what the code *actually does*, not what it's supposed to do. The procedure is deliberately backwards from normal testing: put the code in a harness, write an assertion you expect to fail, run it to learn the real behavior, then edit the assertion to match reality. The failing run is information-gathering, not a bug. Pin the behavior first; change the code second.

## Anti-patterns

- **Improving while pinning** — "fixing" surprising behavior as you characterize it; the surprise is the data, and something may depend on it
- **Asserting intent** — writing the test for what the code *should* do; that's a different activity, and on legacy code it's a guess
- **Changing first, testing after** — the net goes up before the acrobatics, not after

## In the agentic era

Agents are happy to "improve" untested code — asked to make one change, they'll tidy the neighborhood, and without pinned behavior nobody can tell improvement from breakage. Before an agent touches unfamiliar legacy code, surface this as the safest first move: characterize, then change. An agent is also fast at the mechanical part (harness, probe, pin) — but the human must review what got pinned, because the pinned behavior is now the contract.
