# Kata: Walking Skeleton — Event Notification Service

## Format

Design exercise. No code to write. Output is a written description of your walking skeleton.

## System Description

You are starting a new **Event Notification Service**. Its eventual job:

- Accept events via an HTTP API (e.g., `POST /events`)
- Store events in a database
- Send email notifications to registered subscribers when a matching event arrives
- Expose a status endpoint (`GET /health`)

The team uses Python, deploys to a cloud VM via a CI/CD pipeline, and stores data in PostgreSQL. Email is sent via a third-party SMTP service.

The system does not exist yet. No code has been written.

## Your Task

Identify the **walking skeleton** for this system.

Write a description covering:

1. **What is in the skeleton?** Name every component that must exist (HTTP server, database connection, email client, CI pipeline, etc.) and what each does in the skeleton — not in the final system.
2. **What is NOT in the skeleton?** Name at least two things you are explicitly leaving out and why.
3. **How is it deployed?** Describe the deployment target and how you would verify it is reachable.
4. **What is the thinnest end-to-end path?** Describe a single request that touches every layer from HTTP entry point to backing store, without containing business logic.

## Self-Assessment Criteria

Evaluate your walking skeleton against these questions:

| Criterion | Question |
|-----------|----------|
| **End-to-end** | Does a request travel from HTTP entry point through every architectural layer (app → DB, app → email client) to a real backing service? |
| **Deployed** | Is the skeleton reachable through real infrastructure — not just runnable on your laptop? |
| **No business logic** | Does the skeleton contain any event matching, subscriber lookup, or notification routing? If yes, remove it. |
| **Earns the pipeline** | Does a CI pipeline run tests against the deployed target and go green before feature work begins? |
| **Thin enough** | Could you rebuild this skeleton in a day if the architecture turned out to be wrong? |

## Reference Answer

<details>
<summary>Expand after completing your own answer</summary>

**In the skeleton:**
- A Python HTTP server (Flask or FastAPI) with one route: `POST /events` returns `202 Accepted` with a hardcoded body — no event storage, no subscriber lookup
- A `GET /health` endpoint returning `{"status": "ok"}`
- A database connection that runs one query (`SELECT 1`) at startup to verify connectivity — no schema, no tables
- An SMTP client stub that logs "would send email" to stdout — no real email sent
- A Dockerfile that packages the app
- A CI workflow that builds the image, pushes it to a registry, deploys to the VM, and runs `GET /health` against the live URL

**Not in the skeleton:**
- Event schema or storage (no `events` table) — that's a feature
- Subscriber registry — that's a feature
- Notification routing or matching logic — that's a feature
- Any form of authentication — deferred until the first feature that needs it

**Deployed:** The app runs on the cloud VM behind a domain name. CI deploys on every push to `main`. The final CI step hits `https://<domain>/health` and fails the pipeline if it doesn't return `200`.

**Thinnest end-to-end path:** `POST /events` → app layer receives request → DB connection verified at startup (not per-request) → `202 Accepted` returned. The DB touch is at startup rather than per-request because the skeleton's goal is to verify connectivity, not to implement persistence.

**Is it thin enough?** Yes — if PostgreSQL turns out to be the wrong choice, you can swap it before any schema is defined.

</details>
