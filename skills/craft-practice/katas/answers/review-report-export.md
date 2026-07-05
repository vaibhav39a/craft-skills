# ANSWERS — Report Export review kata

**Facilitator/reveal material. Do not open before the written critique is complete.**

Flaw concepts exercised: deep-modules, information-hiding, pull-complexity-downwards, define-errors-out-of-existence, yagni.

## The four planted flaws

1. **Presumptive architecture (yagni + shallow module).** `ReportExporterFactory` is a factory for one format — pure interface with no functionality behind it, built for exporters that don't exist. The "unsupported format" error path serves capability nobody shipped. Cost of carry: every future reader must understand the factory to trace one constructor call.
2. **Temporal decomposition wearing an API (information-hiding + define-errors).** The `prepare()`/`render()` split exposes the exporter's internal sequencing as caller obligations — and `ExportNotPreparedError` exists *only because the API leaked that sequencing*. A single `render(report)` defines the error out of existence and deletes a test with it. The shipped test for this error pins the design flaw in place.
3. **Complexity punted upward (pull-complexity-downwards).** Five constructor knobs (`delimiter`, `quote_char`, `line_ending`, `encoding`, `buffer_size` — the last never even used) are decisions the module should own, pushed to callers who know less than the module about correct CSV. The route then re-punts two of them all the way to the HTTP API as query params — public surface for decisions no requirement asked anyone to make.
4. **Leaked format knowledge (information-hiding, change amplification).** The route hardcodes `media_type="text/csv"` and a `.csv` filename while taking `fmt` as a parameter — the exporter's format knowledge now lives in two places. The day a second format actually arrives, the route breaks silently for it: content type, filename, and factory must all change in sync. Classic change amplification, planted by the factory's own false generality.

## Bonus observations a strong review makes

`test_factory_creates_csv_exporter` asserts a type, not a behavior — it can't fail meaningfully; and the route mutating `exporter.delimiter` after construction bypasses the constructor's apparent contract.
