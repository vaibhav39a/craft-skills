# Report Export — canned review kata (design flaws)

format: review
concept: design review judgment (flaw concepts named in the answers file — reading them here would pre-solve the hunt)
time-box: 20–30 min
source: original to this repo; diff and planted flaws authored by hand. Companion to review-notification-preferences (test-and-discipline flaws); this one's flaws are structural.
answers: answers/review-report-export.md — do not open before the written critique

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

Write the review you'd actually post. There are **four planted design flaws**. For each: name it (craft-coach's concept vocabulary if you have that skill installed; plain design language works too), say what future change it taxes, and say what you'd ask the author for instead. Also state what you'd approve — the quoting logic, for instance, deserves a fair read.

## Rules of engagement

- Full written critique before opening the reveal.
- "It works" is stipulated — every flaw here compiles, passes, and demos fine. Review the *decisions*.

## Variations

1. **Cold read** — as written above.
2. **Change-request framing** — for each flaw, write the single sentence that would get it fixed without prescribing the fix.
3. **Amplification test** — before the reveal, answer: "the product now wants TSV export and a UTF-16 client — which lines change?" Then review again.
4. **Pair with the other review kata** — run review-notification-preferences in the same week; reflect on which flaw *family* (discipline vs design) you catch more reliably.

## Running this with a team

Everyone reviews the same diff independently and writes their critique **before anyone opens the answers file**. Collect all critiques; then open [answers/review-report-export.md](answers/review-report-export.md) together and compare each critique against the key — tallying key-matches is calibration and allowed; judging people isn't. Pair this with review-notification-preferences in the same week and name which flaw family (discipline vs design) the team catches more reliably.

## Reflection prompt

Which flaw did the PR description's language ("clean extensible architecture") pre-emptively defend you out of questioning? What does that tell you about reviewing agent-written justifications?

## Reveal

The planted flaws are in [answers/review-report-export.md](answers/review-report-export.md). Open it only after your written critique.
