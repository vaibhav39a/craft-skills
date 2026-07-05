# Bounded Context

Source: Eric Evans, *Domain-Driven Design* (2003); *DDD Reference* (2015) — provenance: web-sourced (https://www.domainlanguage.com/wp-content/uploads/2016/05/DDD_Reference_2015-03.pdf, https://www.dddcommunity.org/resources/ddd_terms/)

## When it applies

- One model is being stretched to serve parts of the system that mean different things by the same words
- Code based on two different models is about to be combined
- It's unclear where a model *stops* applying

## The rule

Multiple models are inevitable on any large project — don't fight that; make each model's boundary explicit. A bounded context is the boundary (typically a subsystem or a team's work) within which a particular model is defined and applicable. It's a linguistic and model boundary first — model expressions only have meaning in context — not primarily a deployment or service boundary. Evans defines it along three axes at once: team organization, usage within the application, and physical artifacts (code bases, database schemas); keep the model strictly consistent inside, and don't be distracted by what's outside. The payoff: a shared understanding of what must be consistent and what can develop independently.

## Anti-patterns

- **Unknowing model blend** — combining code from distinct models; "software becomes buggy, unreliable, and difficult to understand"
- **Big Ball of Mud** — models mixed, boundaries inconsistent everywhere; Evans's move is to draw a boundary around the mess, name it, refuse sophisticated modeling *inside* it, and guard against its sprawl

## In the agentic era

One-model-rules-all is the agent default: asked to add a feature, it will reuse whatever entity it finds and extend a schema across meanings, because it doesn't *feel* the boundary — the friction humans sense at team and meaning seams is invisible to a context window that spans the whole repo. Boundaries an agent will respect must be declared, not sensed (a context map or per-context glossary the session actually loads). When an agent's edit crosses a boundary or stretches a model to its second meaning, name it.
