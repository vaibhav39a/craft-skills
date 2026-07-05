# Listen to the Tests

Source: Steve Freeman and Nat Pryce, *Growing Object-Oriented Software, Guided by Tests* (2009), ch. 20 — provenance: web-sourced (https://growing-object-oriented-software.com/toc.html; https://www.jmock.org/oopsla2004.pdf, "Mock Roles, not Objects")

## When it applies

- A test is hard to write and the fix being reached for is a fancier test
- Setup is piling up: networks of mocks, bloated fixtures, walls of expectations
- A test needs "magic" (mocking the unmockable) to work at all

## The rule

Test pain is design feedback about the system under test, not a tooling problem. The authors' claim is stronger than "hard tests hint at bad design": mock-based tests *amplify* weak design — tight coupling and misallocated responsibilities show up as test complexity — and forcing the test to pass anyway silences exactly the signal you should be hearing. The GOOS ch. 20 smell catalog maps pain to diagnosis: bloated constructor, too many dependencies, too many expectations, mocking concrete classes, mocking values. Respond by redesigning the SUT, not by elaborating the test.

## Anti-patterns

- **Coping instead of listening** — more helpers, deeper fixtures, cleverer mocks; the test gets quieter and the design stays wrong
- **Mocking through the pain** — tools that mock the unmockable turn a design instrument back into "just a testing technique"
- **Blaming the framework** — the frustration is real; its address is the SUT

## In the agentic era (observed 2026-07)

Agents are tireless test-elaborators: hard-to-test code doesn't frustrate them, so they'll build the mock network a human would have refused to type — and the design signal dies in the fixture. When a test fights back, ask what the pain says about the SUT before making the test smarter. The human's ear for "this test is telling us something" is the craftsperson skill; keep it in the loop rather than coping on their behalf.
