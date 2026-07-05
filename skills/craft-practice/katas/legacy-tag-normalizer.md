# Legacy Tag Normalizer — characterization-tests kata

format: test-driven
concept: characterization-tests
time-box: 30–45 min
source: original to this repo; kata shape follows Feathers's characterization procedure (see the concept file)

## Setup

You've inherited this function. It's in production. Nobody remembers its rules; things depend on whatever it currently does. **You did not write it, and you may not fix it.**

```python
def normalize_tags(tags, limit=None):
    seen = {}
    for tag in tags:
        key = tag.strip().lower().replace(" ", "-")
        if key and key not in seen:
            seen[key] = tag
    result = sorted(seen)
    if limit:
        result = result[:limit]
    return result
```

Put it in a test harness. Then work Feathers's deliberately backwards procedure: write an assertion for what you *expect* it to do, run it **expecting to fail**, read the actual behavior, and edit the assertion to match reality. The failing run is information-gathering, not a bug.

## Goal

A test suite that pins the function's *actual* behavior — including every behavior that surprised you. You're done when you'd be comfortable letting an agent refactor this function with your suite as the net.

## Rules of engagement

1. **Pin, don't fix.** When you find behavior that looks wrong, the test asserts what it *does* — the surprise is the data, and something in production may depend on it. Keep a side list of "suspicious" findings; that list is an output, not a to-do.
2. **Probe with intent.** Before each test, say what question it asks ("what happens at the limit boundary?"). Random inputs are fishing; characterization is interrogation.
3. The facilitator may suggest *directions* to probe ("have you asked about falsy arguments?") but never tells you the behavior.

## Variations

1. **The supplied function** — above. It holds several genuine surprises; find them by running, not by reading alone.
2. **Pin, then change safely** — after variation 1, make one structural change (rename, extract a helper) under your net, tests green throughout. The payoff moment of the whole technique.
3. **Agent-authored legacy** — have an agent write a ~20-line function with three deliberately undocumented quirks (it keeps the list secret). Pin it; then the agent reveals its list and you compare against what your suite caught.
4. **Your own codebase** — pick the scariest small function you actually depend on. Real stakes, same procedure.

## Reflection prompt

Which surprise did you find by *running* that you'd missed by *reading*? And which pinned behavior are you now most worried something depends on?
