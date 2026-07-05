# Test-Pain Diagnosis — listen-to-the-tests kata

format: pattern-recognition
concept: listen-to-the-tests
time-box: 25–40 min
source: pain taxonomy from Freeman & Pryce, *GOOS* ch. 20 (see the concept file's cited sources); kata shape from the predecessor repo's design ("a diagnosis exercise, not a fix exercise")

## Setup

The facilitator presents 4–6 test excerpts (with just enough of the system under test to read them). Each test *passes*. Each was written by someone competent who was coping with something. Your job is not to improve the tests — it's to hear what the coping conceals.

## Goal

For each sample, a written **diagnosis**: name the pain (what made this test hard to write), name the design signal it carries (what the SUT's structure is saying), and state the question you'd take to the SUT's owner. **No fixes, no refactored versions** — recognizing the signal is the skill; the fix is downstream and out of scope.

The GOOS pain → signal vocabulary, for naming what you find:

| Pain in the test | What it signals about the SUT |
|---|---|
| Bloated constructor / heavy setup | Too many responsibilities feeding construction |
| A network of mocks to get one assertion | Object navigates a web of dependencies; misallocated responsibilities |
| Too many expectations | The test knows too much about *how*; the object orchestrates too much |
| Mocking a concrete class | A missing role — the relationship has no name of its own |
| Needing "magic" to mock the unmockable | A hidden dependency (global, static, buried construction) |
| Elaborate fixtures for values | A value type that wants to exist and doesn't |

## Rules of engagement

1. Diagnose before the facilitator comments; the justification matters more than the label.
2. "This test is fine" is a valid diagnosis — some samples may carry no signal; false positives cost as much as misses.
3. The facilitator probes ("what would have to change about the SUT for this setup to disappear?") and reveals the intended reading only at the end.

## Variations

1. **Taxonomy diet** — samples built one-per-row from the table above.
2. **Your own suite** — bring your slowest or most brittle real test; diagnose it cold.
3. **Agent-coped tests** — have an agent write tests for a deliberately hard-to-test class; it will cope heroically (fixtures, mock networks) rather than complain. Diagnose what its coping buried.
4. **One SUT, three test styles** — the same awkward class tested three different ways; identify which style *silences* the signal and which lets it through.

## Reflection prompt

Which pain do you routinely cope with in your own work rather than hear? What's the standing question you should be asking when a test fights back?
