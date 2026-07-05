# Smell Spotting

format: pattern-recognition
concept: code-smells
time-box: 20–40 min

## Setup

The facilitator presents 6–10 short code samples (10–40 lines each). Some carry a classic smell — long parameter list, feature envy, data clump, divergent change, shotgun surgery, primitive obsession — some are honestly fine. The mix is not announced.

## Goal

For each sample: say whether it smells, name the smell if you can, and — the actual skill — say what deeper design problem the smell *signals* and what question you'd ask before touching it. "No smell" is a valid and scored answer; false positives matter as much as misses.

## Rules of engagement

- Judge before the facilitator comments; naming the signal beats naming the catalog term.
- A smell is an invitation to look, not a rule to fix — for each smell found, say whether you'd act now, note it, or leave it, and why.
- The facilitator probes justifications ("what change would this code punish?") and reveals the intended reading only at the end.

## Variations

1. **Catalog diet** — samples built around the classic Fowler & Beck smells, one each.
2. **Clean control group** — half the samples deliberately smell-free; practice saying "this is fine."
3. **Your own codebase** — pull real functions from work you own; classify them cold.
4. **Agent-generated** — have an agent implement a small feature, then smell-spot its output; agents produce syntactically clean code whose smells are structural, not cosmetic.
5. **Same smell, three costumes** — one smell (e.g. feature envy) appearing in three different domains; practice recognizing the shape, not the surface.

## Reflection prompt

Which smell did you miss or over-call, and what cue were you relying on? Where in your current work does the "act now, note it, or leave it" judgment feel hardest?
