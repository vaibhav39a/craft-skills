# SAMPLE BANK + KEY — Module Depth kata

**Facilitator material.** Present samples one at a time — interface and note only, **never the verdict** — in roughly this order (difficulty ramps). Reveal verdicts only at the end. Ground the reveal in the concept file (`../craft-coach/concepts/design/deep-modules.md`) if installed.

Deliberately excluded: Unix file I/O — it's the worked example named inside the concept file, a memorized freebie for anyone who did the reading.

---

**S1.** `send_email(to, subject, body) -> MessageId`
*Note:* the implementation manages connection pooling, retry with backoff, MIME encoding, and provider throttling. Callers make one call.
**Verdict: deep.** Three parameters hide five hard problems; the interface says nothing about any of them — that silence is the depth.

**S2.** `EmailClientFactory.create(cfg) -> EmailClient`, then `client.connect()`, `.authenticate()`, `.build_message(...)`, `.send()`, `.disconnect()`
*Note:* each method is short and well-documented; calls must happen in this order.
**Verdict: shallow.** Six-step interface for one job — the module's internal *sequence* is the caller's problem (temporal decomposition leaking as API). Compare S1: same functionality, opposite depth.

**S3.** `JsonConfig.parse(text)` — a class whose entire implementation is `return json.loads(text)`.
*Note:* introduced "so we can swap JSON libraries later."
**Verdict: shallow** — the pass-through wrapper: invoking it costs as much as inlining it, and the swap-later rationale is a presumptive feature.

**S4.** `Money(amount, currency)` with `+`, `*`, and `allocate(ratios) -> [Money]`.
*Note:* small class; `allocate` distributes remainders so that no cent is created or lost.
**Verdict: deep.** The interface is a few operators; behind `allocate` sits the penny-allocation problem every naive implementation gets wrong. Depth isn't size — it's the ratio.

**S5.** `retry(fn, attempts=3, backoff=2.0, retry_on=(TimeoutError,))`
*Note:* implements jittered exponential backoff and deadline propagation; defaults chosen for the common case.
**Verdict: deep, and deliberately *somewhat* generic** — usable beyond today's caller without becoming a framework. Good discussion sample: would an `attempts`-only signature be deeper or just less honest?

**S6.** `UserRow` — twelve typed fields, no methods, generated from the DB schema; used only at the persistence boundary.
*Note:* other modules receive a `User` domain object built from it.
**Verdict: legitimately shallow — and fine.** A data carrier at a boundary hides nothing *by design*. The lesson: "shallow" is a diagnosis, not a verdict; the sin is shallow modules multiplying where depth was available.

**S7.** `process(data, options: dict)` — one function, two parameters.
*Note:* `options` has nine documented keys; three change the return type; two interact ("`merge` is ignored unless `sort` is set").
**Verdict: shallow in disguise.** The *formal* interface is tiny; the *real* interface — everything a caller must know — is nine keys and their interactions. Interface means cognitive load, not parameter count. The hardest sample; expect disagreement, demand the caller-burden argument.

**S8.** `Cache.get(key, loader, ttl=300)`
*Note:* handles stampede protection (single flight), serialization, and eviction internally; `loader` is called on miss.
**Verdict: deep.** One method absorbs the three failure modes every hand-rolled cache hits. Compare S3: both are "small wrappers" by line count; the difference is what's behind the interface.

---

## Calibration notes

Strong classification arguments cite **caller burden** (what must I know/do to use this?) and **information hidden** (what decision could change without touching me?) — not line counts. S6 and S7 are the discriminators: S6 tests whether "shallow" is reflexively treated as bad; S7 tests whether "small signature" is reflexively treated as deep.
