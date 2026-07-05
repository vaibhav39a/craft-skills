# SAMPLE BANK + KEY — Smell Spotting kata

**Facilitator material.** Present samples one at a time — code only, **never the verdict** — mixed order, without announcing how many are clean. Reveal at the end, grounded in the concept file (`../craft-coach/concepts/refactoring/code-smells.md`) if installed. "No smell" answers count in calibration; false positives matter as much as misses.

---

**A.**
```python
class InvoiceFormatter:
    def total_for(self, customer):
        total = 0
        for order in customer.orders:
            for line in order.lines:
                total += line.qty * line.unit_price
        return total - customer.loyalty_discount(total)
```
**Verdict: smell — feature envy.** The formatter computes exclusively from `customer`'s and `order`'s data; the calculation wants to live on those objects. Signal: misallocated responsibility. Act now? Ask first where else totals are computed — envy often marks a missing domain method several callers want.

**B.**
```python
def create_shipment(street, city, postcode, country, weight_kg):
    ...

def validate_address(street, city, postcode, country):
    ...

def format_label(name, street, city, postcode, country):
    ...
```
**Verdict: smell — data clump.** The same four fields travel as a pack through three signatures. Signal: an `Address` type wants to exist; until it does, every address rule is smeared across call sites. Note it or act — the third repetition is usually the act-now threshold.

**C.**
```python
def business_days_between(start: date, end: date) -> int:
    """Count weekdays in [start, end), ignoring holidays."""
    days = 0
    current = start
    while current < end:
        if current.weekday() < 5:
            days += 1
        current += timedelta(days=1)
    return days
```
**Verdict: clean.** Small, named honestly, one job, documented limitation. If someone flags the loop as "inefficient," that's a performance conversation, not a smell — the design says nothing untrue.

**D.**
```python
def apply_permissions(user, resource):
    if user.role == "admin":
        return Permission.ALL
    elif user.role == "editor":
        return Permission.READ | Permission.WRITE
    elif user.role == "viewer":
        return Permission.READ
    # roles checked the same way in auth.py, export.py, audit.py
```
**Verdict: smell — primitive obsession (with shotgun surgery in the comment).** `role` is a string compared against literals in four files; adding a role is a four-file change. Signal: a `Role` type with its own permission knowledge wants to exist. The comment is the tell — this one is usually act-now.

**E.**
```python
def render_header(title, author, date, font, size, margin_top,
                  margin_bottom, color, align="left"):
    ...
```
**Verdict: smell — long parameter list, two clumps.** (`font`, `size`, `color`, `align`) is a `TextStyle`; (`margin_top`, `margin_bottom`) is spacing. Signal: missing value objects. Mild on its own — the question to ask is whether these packs recur across the rendering API.

**F.**
```python
class Settings:
    def parse_cli_args(self, argv): ...
    def load_from_database(self, conn): ...
    def render_admin_html(self): ...
    def as_env_exports(self): ...
```
**Verdict: smell — divergent change.** One class changes for four unrelated reasons (CLI conventions, schema, admin UI, shell format). Signal: four responsibilities sharing a name because they all touch "settings." The fix direction is separation — but the diagnosis, not the split, is today's job.

**G.**
```python
def bootstrap_worker(config):
    logging.basicConfig(level=config.log_level)
    db = connect_db(config.dsn, pool_size=config.pool)
    queue = connect_queue(config.broker_url)
    register_signal_handlers()
    warm_cache(db, config.cache_keys)
    return Worker(db=db, queue=queue, config=config)
```
**Verdict: clean — the "long = smell?" trap.** Fifteen straight-line steps of startup narrative, each line one idea, order genuinely required. Fowler's *usually* cuts both ways: some long functions are legitimate. Splitting this into six one-line functions would *add* obscurity.

**H.**
```python
class OrderService:
    def __init__(self, repo):
        self._repo = repo
    def get(self, order_id):
        return self._repo.get(order_id)
    def save(self, order):
        return self._repo.save(order)
    def delete(self, order_id):
        return self._repo.delete(order_id)
```
**Verdict: smell — middle man.** Every method delegates; the "service" adds a name and nothing else. Signal: either a layer imposed by convention rather than need, or a class waiting for behavior that never arrived. Ask what was *supposed* to live here before deleting it.

---

## Calibration notes

Two samples are clean (C, G) — both bait a reflexive flag (loop "inefficiency", function length). Strong answers name the *signal*, not just the catalog term, and end with a defensible act-now / note-it / leave-it call. A perfect catalog score with no signal-naming is the **catalog worship** anti-pattern doing the kata.
