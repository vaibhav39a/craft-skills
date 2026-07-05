# Walking Skeleton

Source: term coined by Alistair Cockburn (*Crystal Clear*, 2004); developed in Steve Freeman and Nat Pryce, *Growing Object-Oriented Software, Guided by Tests* (2009) — provenance: author-verified (GOOS reading)

## When it applies

- A new project or service has features to build but no working end-to-end path through real infrastructure
- Business logic is about to be written before the deployment pipeline, test harness, or integration plumbing exists

## The rule

Before features, earn a deployed, end-to-end path: touching every architectural layer (stub responses are fine), reachable by a real consumer through real infrastructure, with CI green against the deployed target. No business logic in the skeleton — its job is to prove the path, not deliver value. Thin enough to rebuild in a day if the approach turns out wrong. Distinguish it from a spike (throwaway, not deployed), a tracer bullet (may not require deployment), and an MVP (includes user value).

## Anti-patterns

- **Local-only skeleton** — runs on your laptop; the deployment pipeline was the point
- **Feature creep before the skeleton is done** — debt accumulating on an unverified foundation
- **Skeleton-as-MVP** — "just enough logic to show stakeholders" collapses proving-the-path into delivering-value
- **Declaring victory at "it runs"** — done means CI green against the deployed target

## In the agentic era

Agents scaffold impressive local-only apps in minutes — which makes **Local-only skeleton** the default failure, not the exception. When asked to "build the skeleton," surface that it isn't one until it's deployed and reachable, and offer the deployment configuration before any feature. When feature work is requested against an undeployed skeleton, name **Feature creep before the skeleton is done** and let the human accept the debt consciously or build the path first.
