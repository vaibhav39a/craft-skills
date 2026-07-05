# ANSWERS — Notification Preferences review kata

**Facilitator/reveal material. Do not open before the written critique is complete.**

Flaw concepts exercised: two-hats, yagni, self-testing-code, define-errors-out-of-existence.

## The four planted flaws

1. **Silent behavior change inside the "refactor" (two-hats).** The notification threshold moved from `severity >= 2` to a default `min_severity` of **3** during the "cleanup." Severity-2 events silently stop notifying. The PR description calls this a refactor; it is a behavior change wearing a refactor's clothes — and no test covers the default threshold, so CI stays green.
2. **A test that can't meaningfully fail (self-testing-code).** `test_min_severity_configurable` asserts the constructor stored the value — it passes even if `should_notify` ignores `min_severity` entirely. It's coverage theater: the behavior (configured threshold actually gating notifications) is never exercised.
3. **Speculative capability (yagni).** `SUPPORTED_CHANNELS` accepts and stores `"sms"` and `"push"` — channels nothing in the system can send. A presumptive feature: users can now configure behavior that doesn't exist, and the stored values become a compatibility constraint before the feature is ever built.
4. **Swallowed failure (define-errors-out-of-existence, inverted).** `_get_preferences` catches *all* exceptions and returns `{}` — a user object in a broken state now silently gets default notification behavior instead of surfacing the bug. This is defensive programming punting a real error into invisible misbehavior, the opposite of designing the error out.

## Bonus observations a strong review also makes

`user.preferences.update(body)` writes arbitrary request keys into preferences (no allowlist — `body` could set anything), and the roundtrip test asserts only the status code, not that the preference took effect.
