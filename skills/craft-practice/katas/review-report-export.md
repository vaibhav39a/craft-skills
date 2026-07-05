# Report Export — canned review kata (design flaws)

format: review
concept: design review judgment (deep-modules, information-hiding, pull-complexity-downwards, define-errors-out-of-existence, yagni)
time-box: 20–30 min
source: original to this repo; diff and planted flaws authored by hand. Companion to review-notification-preferences (test-and-discipline flaws); this one's flaws are structural.

## Setup

An agent was asked: *"Add CSV export for reports."* It produced the PR below. Tests pass, CI is green, and — this matters — **every line is locally reasonable and nothing is a bug.** The flaws here are design decisions, which is why review is the only place they can be caught.

**PR description (the agent's):** "Adds report export with a clean extensible architecture: an exporter factory, a configurable CsvExporter, and an export endpoint. Includes tests."

```diff
--- /dev/null
+++ b/app/export.py
@@ -0,0 +1,34 @@
+class ExportNotPreparedError(Exception):
+    pass
+
+
+class ReportExporterFactory:
+    def create(self, fmt):
+        if fmt == "csv":
+            return CsvExporter()
+        raise ValueError(f"unsupported format: {fmt}")
+
+
+class CsvExporter:
+    def __init__(self, delimiter=",", quote_char='"', line_ending="\r\n",
+                 encoding="utf-8", buffer_size=8192):
+        self.delimiter = delimiter
+        self.quote_char = quote_char
+        self.line_ending = line_ending
+        self.encoding = encoding
+        self.buffer_size = buffer_size
+        self._rows = None
+
+    def prepare(self, report):
+        self._rows = [report.columns] + report.rows
+
+    def render(self):
+        if self._rows is None:
+            raise ExportNotPreparedError("call prepare() before render()")
+        lines = [self.delimiter.join(self._quote(v) for v in row)
+                 for row in self._rows]
+        return self.line_ending.join(lines).encode(self.encoding)
+
+    def _quote(self, value):
+        v = str(value).replace(self.quote_char, self.quote_char * 2)
+        return f"{self.quote_char}{v}{self.quote_char}"

--- a/app/routes.py
+++ b/app/routes.py
@@ -58,6 +58,16 @@
+@app.get("/reports/{report_id}/export")
+def export_report(report_id: int, fmt: str = "csv",
+                  delimiter: str = ",", encoding: str = "utf-8"):
+    report = load_report_or_404(report_id)
+    exporter = ReportExporterFactory().create(fmt)
+    exporter.delimiter = delimiter
+    exporter.encoding = encoding
+    exporter.prepare(report)
+    body = exporter.render()
+    return Response(body, media_type="text/csv",
+                    headers={"Content-Disposition":
+                             f"attachment; filename=report-{report_id}.csv"})

--- a/tests/test_export.py
+++ b/tests/test_export.py
@@ -0,0 +1,9 @@
+def test_factory_creates_csv_exporter():
+    exporter = ReportExporterFactory().create("csv")
+    assert isinstance(exporter, CsvExporter)
+
+def test_render_requires_prepare():
+    with pytest.raises(ExportNotPreparedError):
+        CsvExporter().render()
```

## Goal

Write the review you'd actually post. There are **four planted design flaws**. For each: name it (the concept vocabulary in `craft-coach/concepts/` is the intended language), say what future change it taxes, and say what you'd ask the author for instead. Also state what you'd approve — the quoting logic, for instance, deserves a fair read.

## Rules of engagement

- Full written critique before opening the reveal.
- "It works" is stipulated — every flaw here compiles, passes, and demos fine. Review the *decisions*.

## Variations

1. **Cold read** — as written above.
2. **Change-request framing** — for each flaw, write the single sentence that would get it fixed without prescribing the fix.
3. **Amplification test** — before the reveal, answer: "the product now wants TSV export and a UTF-16 client — which lines change?" Then review again.
4. **Pair with the other review kata** — run review-notification-preferences in the same week; reflect on which flaw *family* (discipline vs design) you catch more reliably.

## Reflection prompt

Which flaw did the PR description's language ("clean extensible architecture") pre-emptively defend you out of questioning? What does that tell you about reviewing agent-written justifications?

## Reveal — planted flaws

<details>
<summary>Open only after your written critique</summary>

1. **Presumptive architecture (yagni + shallow module).** `ReportExporterFactory` is a factory for one format — pure interface with no functionality behind it, built for exporters that don't exist. The "unsupported format" error path serves capability nobody shipped. Cost of carry: every future reader must understand the factory to trace one constructor call.
2. **Temporal decomposition wearing an API (information-hiding + define-errors).** The `prepare()`/`render()` split exposes the exporter's internal sequencing as caller obligations — and `ExportNotPreparedError` exists *only because the API leaked that sequencing*. A single `render(report)` defines the error out of existence and deletes a test with it. The shipped test for this error pins the design flaw in place.
3. **Complexity punted upward (pull-complexity-downwards).** Five constructor knobs (`delimiter`, `quote_char`, `line_ending`, `encoding`, `buffer_size` — the last never even used) are decisions the module should own, pushed to callers who know less than the module about correct CSV. The route then re-punts two of them all the way to the HTTP API as query params — public surface for decisions no requirement asked anyone to make.
4. **Leaked format knowledge (information-hiding, change amplification).** The route hardcodes `media_type="text/csv"` and a `.csv` filename while taking `fmt` as a parameter — the exporter's format knowledge now lives in two places. The day a second format actually arrives, the route breaks silently for it: content type, filename, and factory must all change in sync. Classic change amplification, planted by the factory's own false generality.

Bonus observations a strong review makes: `test_factory_creates_csv_exporter` asserts a type, not a behavior — it can't fail meaningfully; and the route mutating `exporter.delimiter` after construction bypasses the constructor's apparent contract.

</details>
