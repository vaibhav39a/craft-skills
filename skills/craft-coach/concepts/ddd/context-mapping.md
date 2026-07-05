# Context Mapping

Source: Eric Evans, *DDD Reference* (2015), Part IV "Context Mapping for Strategic Design" — provenance: web-sourced (https://www.domainlanguage.com/wp-content/uploads/2016/05/DDD_Reference_2015-03.pdf, https://www.dddcommunity.org/resources/ddd_terms/)

## When it applies

- Multiple bounded contexts (or teams, or systems) are in play and their relationships have never been named
- An integration is being designed as if one model ruled everywhere
- A dependency on another team's model is shaping your own without anyone deciding that

## The rule

Identify every model in play — including the implicit models of legacy subsystems — define each one's bounded context, name it into the ubiquitous language, and describe the points of contact: where translation happens, what's shared, who influences whom. **Map the existing terrain; take up transformations later** — the map documents what *is*, not the target architecture. The relationships are as organizational as technical (Evans: constraints between contexts manifest "primarily through non-technical channels"), and they have names: partnership, shared kernel, customer/supplier, conformist, anticorruption layer, open-host service, published language, separate ways — plus the upstream/downstream vocabulary underneath them. Choosing one is a strategic decision, and "separate ways" is a legitimate choice: integration is always expensive, and sometimes the benefit is small.

## Anti-patterns

- **Unmapped terrain** — edges blur, interconnections complicate, contexts "bleed into each other" because nobody holds the large-scale view
- **Aspirational map** — drawing the architecture you want instead of the relationships that exist
- **Accidental conformist** — adopting an upstream's model by drift rather than by decision

## In the agentic era (observed 2026-07)

Agents make accidental relationships at generation speed: an integration drafted against an upstream API quietly conforms to its model, or copies enough of it to create an unagreed shared kernel — pattern choices made by no one. The flip side: anticorruption layers, historically expensive to justify, are now cheap to build — so the human's job is the strategic call the agent can't make (*which* relationship should this be?), and the agent's job is the translation code. When generated integration code lets another context's model leak into yours, name the drift and ask which named relationship was actually intended.
