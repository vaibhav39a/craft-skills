# Event Notification Service — walking-skeleton kata

format: reflective
concept: walking-skeleton
time-box: 30–45 min

## Setup

A design-journaling exercise: you write a walking-skeleton plan and stress it against the concept's rules. Default scenario (variation 1) — a new **Event Notification Service**: accepts events via HTTP (`POST /events`), stores them in PostgreSQL, emails registered subscribers on matching events, exposes `GET /health`. Python, cloud VM, CI/CD pipeline, third-party SMTP. No code exists yet.

## Goal

A written skeleton description covering four things: what's *in* the skeleton (every component, and what it does in the skeleton, not the final system); what's explicitly *out* and why (at least two); how it's deployed and verified reachable; and the thinnest end-to-end path — one request touching every layer with zero business logic.

## Rules of engagement

- Write your full answer before opening the facilitator notes.
- Self-assess against the concept's rules: end-to-end through real infrastructure? CI green against the deployed target? No business logic anywhere? Rebuildable in a day?
- The facilitator prompts and probes ("does that DB touch actually verify the path?") but never drafts your skeleton.

## Variations

1. **Supplied scenario** — the Event Notification Service above.
2. **Your next real project** — the reflective ideal: whatever you're actually about to start; the skeleton plan becomes real work.
3. **Legacy variant** — a system that runs locally but has never been deployed; plan the skeleton it never earned.
4. **Agent-scaffold audit** — have an agent scaffold the scenario, then assess its output against your skeleton plan: what did it build locally that proves nothing end-to-end?

## Reflection prompt

One paragraph: which part of the path were you most tempted to fake locally, and what integration risk would that have deferred?

## Facilitator comparison notes

<details>
<summary>Open only after writing your own synthesis</summary>

A strong answer typically includes: one route returning a hardcoded `202`, a health endpoint, a startup connectivity check (`SELECT 1`) with no schema, an SMTP stub logging "would send," a Dockerfile, and CI that builds, deploys, and fails the pipeline unless `GET /health` returns 200 against the live URL. Explicitly out: event schema/storage, subscriber registry, matching/routing logic, auth — all features. The common miss: putting the DB touch per-request instead of at startup (the skeleton verifies connectivity, not persistence) — either is defensible if the *reasoning* names what's being proven.

</details>
