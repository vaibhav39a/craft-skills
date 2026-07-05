# Aggregates

Source: Eric Evans, *Domain-Driven Design* (2003); *DDD Reference* (2015), Part II — provenance: web-sourced (https://www.domainlanguage.com/wp-content/uploads/2016/05/DDD_Reference_2015-03.pdf, https://www.dddcommunity.org/resources/ddd_terms/)

## When it applies

- Changing one object can silently break invariants involving its conceptual parts
- A transaction is growing to touch many entities "to be safe"
- Anything can reference anything in the object model, and locking or distribution is getting painful

## The rule

Cluster entities and value objects into aggregates — units of change with explicit boundaries. One entity is the root: external objects hold references only to the root (internal references may pass out for a single operation only), and the root enforces the aggregate's invariants. The boundary is operational, straight from Evans: **within an aggregate, apply consistency rules synchronously; across aggregates, handle updates asynchronously** — and keep an aggregate together on one server while distributing different aggregates freely. When transactions or distribution fight the boundaries, don't fight back with machinery: reconsider the model — the friction usually hints at a missing domain insight.

## Anti-patterns

- **Blindsided objects** — state corrupted by changes to conceptually constituent parts nobody guarded
- **Pointless interference** — cautious lock-everything schemes making multiple users collide until the system is unusable
- **Reference free-for-all** — every object reachable from everywhere, so no boundary means anything

## In the agentic era

Generated CRUD is a reference free-for-all by default: an agent wiring ORM entities will relate anything to anything, and consistency boundaries appear nowhere in the diff because no test or type demands them. When an agent's transaction spans what are really two aggregates, or a generated model hands out references to internals, name the missing boundary. And keep the human in the feedback loop Evans describes: aggregate friction is *model* feedback — an agent will happily add retry logic and distributed locks where the honest fix is a different boundary.
