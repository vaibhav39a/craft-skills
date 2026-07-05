# Notification Preferences — canned review kata

format: review
concept: code review judgment (flaw concepts named in the answers file — reading them here would pre-solve the hunt)
time-box: 20–30 min
source: original to this repo; diff and planted flaws authored by hand
answers: answers/review-notification-preferences.md — do not open before the written critique

## Setup

An agent was asked: *"Add an endpoint so users can update their notification preferences, and clean up NotificationService while you're in there."* It produced the PR below. The tests pass. CI is green.

**PR description (the agent's):** "Adds `PUT /users/{id}/preferences`. Refactored NotificationService to use injectable config for testability. Added tests."

```diff
--- a/app/notifications.py
+++ b/app/notifications.py
@@ -1,12 +1,28 @@
 class NotificationService:
-    def should_notify(self, user, event):
-        if user.preferences.get("notifications") == "off":
-            return False
-        return event.severity >= 2
+    def __init__(self, config=None):
+        self.config = config or {}
+        self.min_severity = self.config.get("min_severity", 3)
+
+    def should_notify(self, user, event):
+        prefs = self._get_preferences(user)
+        if prefs.get("notifications") == "off":
+            return False
+        return event.severity >= self.min_severity
+
+    def _get_preferences(self, user):
+        try:
+            return user.preferences or {}
+        except Exception:
+            return {}

--- a/app/routes.py
+++ b/app/routes.py
@@ -40,6 +40,17 @@
+SUPPORTED_CHANNELS = ("email", "sms", "push")
+
+@app.put("/users/{user_id}/preferences")
+def update_preferences(user_id: int, body: dict):
+    user = get_user_or_404(user_id)
+    if body.get("channel") and body["channel"] not in SUPPORTED_CHANNELS:
+        raise HTTPException(422, "unsupported channel")
+    user.preferences.update(body)
+    save(user)
+    return {"ok": True}

--- a/tests/test_notifications.py
+++ b/tests/test_notifications.py
@@ -12,3 +12,17 @@
+def test_off_preference_suppresses_notification():
+    service = NotificationService()
+    user = Mock()
+    user.preferences = {"notifications": "off"}
+    assert service.should_notify(user, Mock(severity=5)) is False
+
+def test_min_severity_configurable():
+    service = NotificationService({"min_severity": 5})
+    assert service.min_severity == 5
+
+def test_update_preferences_roundtrip(client):
+    resp = client.put("/users/1/preferences", json={"notifications": "on"})
+    assert resp.status_code == 200
```

## Goal

Write your review as you actually would — the comments you'd post, each anchored to a line, each naming what's wrong *and why it matters*. There are **four planted flaws**. Find as many as you can; also say what you'd approve, because knowing what's fine is half the skill.

## Rules of engagement

- Full written critique before opening the reveal. No peeking.
- The facilitator answers questions about the *scenario* (what the app does), never about flaw locations or count beyond what's stated here.

## Variations

1. **Cold read** — as written above.
2. **Severity ranking** — after finding flaws, rank them by blast radius and argue the order.
3. **Ten-minute gate** — time-box to 10 minutes; practice for real review conditions.
4. **Fix-forward** — after the reveal, write the review comment that would get each flaw fixed *without* doing the fix yourself.

## Running this with a team

Everyone reviews the same diff independently and writes their critique **before anyone opens the answers file**. Collect all critiques; then open [answers/review-notification-preferences.md](answers/review-notification-preferences.md) together and compare each critique against the key — tallying key-matches is calibration and allowed; judging people isn't. Close by naming which flaw *family* the team systematically misses, and log per-person lines in PRACTICE.md (Who column).

## Reflection prompt

Which flaw did the green CI most effectively hide from you? What would you add to your personal review checklist as a result?

## Reveal

The planted flaws are in [answers/review-notification-preferences.md](answers/review-notification-preferences.md). Open it only after your written critique.
