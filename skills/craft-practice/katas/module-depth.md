# Module Depth

format: pattern-recognition
concept: deep-modules
time-box: 20–40 min

## Setup

The facilitator presents 6–10 interface samples — function or class signatures with a one-paragraph note on what the implementation does and what callers must do around it. No implementation bodies: depth is judged from the interface's size relative to the functionality it hides.

## Goal

For each sample, classify **deep** or **shallow**, with a justification that names the cues: how much functionality sits behind the interface, what information the interface hides or leaks, how much burden lands on the caller (setup, ordering constraints, error handling, configuration).

## Rules of engagement

- Classify before the facilitator comments; the justification matters more than the verdict.
- "It depends" is allowed only with the missing fact named ("depends whether callers ever need X").
- The facilitator probes ("what would change about this interface if it were deeper?") and only reveals the distinguishing cues at the end.

## Variations

1. **Standard library diet** — samples drawn from real standard-library APIs in a language you know well.
2. **Invented pairs** — the same functionality presented twice, once deep, once shallow; spot which is which and say why.
3. **Your own codebase** — pick modules from work you own; classify them cold, then check against how often their callers change.
4. **Agent-generated** — have an agent scaffold a small feature, then classify every module it created. Agents tend toward many small pass-through classes; find them.
5. **Redesign round** — after classifying, take one shallow sample and sketch (not implement) the deeper interface.

## Reflection prompt

Which cue did you rely on most — interface size, information hiding, or caller burden? Which sample surprised you, and what does that say about the codebases that trained your instincts?
