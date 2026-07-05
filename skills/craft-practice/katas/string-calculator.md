# String Calculator — kata for Red → Green → Refactor

```yaml
format: test-driven
time-box: ~30 min
source: Roy Osherove's String Calculator kata (https://osherove.com/tdd-kata-1), adapted
```

## Setup

You're going to build a function `add(numbers)` that returns the sum of the numbers contained in a string. The variations below tighten and extend its behavior step by step. The kata is *not* about getting to the final variation — it's about practicing the **cycle** on each step: a failing test, the smallest implementation that turns it green, a refactor that doesn't change behavior.

**Language:** use any language with a fast test runner you're comfortable with — the kata is about the cycle, not the language. A Python+`unittest` shape is shown below as one concrete example, but you should substitute your own:

```python
# string_calculator_test.py
import unittest
from string_calculator import add

class StringCalculatorTest(unittest.TestCase):
    def test_empty_string_returns_zero(self):
        self.assertEqual(0, add(""))

if __name__ == "__main__":
    unittest.main()
```

```python
# string_calculator.py
def add(numbers):
    raise NotImplementedError
```

Run the test (`python -m unittest`). It should fail with the implementation error — that's your first red bar. From here, follow the cycle.

## Goal

You've practiced the cycle when you can describe, after the session: which step turned red unexpectedly, where you used *fake-it* (constant return) before generalizing, and one place where the code resisted a refactor — and what that resistance taught you about the design.

You have *not* succeeded just by reaching the final variation. Reaching it without the cycle (TAD-style: implementation first, tests after) doesn't count.

## Rules of engagement

1. **Tests must run between every step.** If you make a change and don't run the tests, you're outside the cycle.
2. **No production code without a failing test in front of you.** If you find yourself editing the implementation without a red bar driving the change, stop and write the test first.
3. **Refactor only with all tests green.** If a refactor makes a test red, revert and try a smaller move.
4. **Smallest implementation wins.** Constant returns are encouraged for the first green; let the second test pull generality out of the code (this is *triangulation*, a sibling concept — if you reach for it, name it).
5. **Time-box is firm.** When the timer rings, stop wherever you are. Reflection happens on whatever cycles you completed — not on whether you finished the kata.
6. **Commit (or stash) at every green.** A green bar is a save point. If a refactor blows up, revert is one command away.

## Variations

Pick one variation per session. Rotate on subsequent runs. Each is a self-contained 30-minute target; don't try to chain multiple in a single session.

### Variation 1 — Empty and one number

**Test list to externalize before starting:**
- `add("")` returns `0`
- `add("1")` returns `1`
- `add("3")` returns `3`

**Goal:** Red → Green → Refactor on three trivial cases. The whole point is to *feel* the rhythm with no domain difficulty in the way.

**Watch for:** the temptation to skip the first cycle ("it's obvious"). Don't. The cycle's value is the discipline of running it on the easy cases too.

### Variation 2 — Two numbers, comma-separated

**Test list:**
- (cases from V1 still pass)
- `add("1,2")` returns `3`
- `add("3,4")` returns `7`

**Goal:** Move from a single number to two numbers via a *single* test. Watch how the implementation generalizes — most learners over-generalize on the first green. Triangulate: write the second case (`"3,4"`) and see whether the code already passes it.

**Watch for:** *Big-step green* — implementing a `split(",")`-and-`sum` solution from one test. Smaller move: read both numbers individually with a constant separator. Let the third test (variation 3) force the loop.

### Variation 3 — Arbitrary count of numbers

**Test list:**
- (V1, V2 cases still pass)
- `add("1,2,3,4,5")` returns `15`
- `add("0,0,0")` returns `0`

**Goal:** Generalize from two numbers to any count. This is where the loop emerges. Notice whether your refactor before this variation already accommodated the loop or whether the loop *forced* a refactor. Both are honest; the rhythm is what matters.

**Watch for:** the design decision of where the parsing lives. Does `add` parse and sum in one function, or does parsing pull out into a helper? The decision should be driven by a refactor on green, not by a speculative architecture choice.

### Variation 4 — Newline as alternative delimiter

**Test list:**
- (V1–V3 cases still pass)
- `add("1\n2,3")` returns `6`
- `add("1\n2\n3")` returns `6`

**Goal:** Add a second delimiter. The implementation's parser is now under design pressure — does it accommodate the new delimiter cleanly, or does it fight you? If it fights, that's design feedback; refactor (on green!) before adding the test for newlines.

**Watch for:** the urge to add the newline support *before* writing the failing test. The cycle says: write the test that proves the feature is missing, then add the support.

### Variation 5 — Reject negative numbers

**Test list:**
- (V1–V4 cases still pass)
- `add("-1,2")` raises (or returns an error per your language's idiom) with a message naming `-1`
- `add("-1,-2,3")` raises with a message naming both negatives
- `add("1,2,3")` continues to work

**Goal:** Introduce error behavior. The first error case is straightforward; the second (collecting *all* negatives in the message) is a real design move — you can't fake-it your way through with a single sentinel. The cycle holds: red on the first negative case, green minimally, then the second negative case forces the collection design.

**Watch for:** test-shape decisions. How does the test assert on the error message? If the assertion is brittle (exact string match), refactor it (on green!) toward something stable (substring or list-of-negatives) before adding the next case.

### Variation 6 — Fake it, on purpose

**Test list:** re-run V1 + V2's cases in a fresh file — but under one extra rule: **every first green must be a hardcoded constant**, even when the real implementation is obvious. After each green, narrate the transform out loud: which duplication between test data and code are you eliminating as the constant becomes an expression?

**Goal:** feel the deliberate friction of returning `0` when you know the answer. This variation makes *fake-it* the focus rather than a passing move — the restraint muscle it builds is for the day the real answer *isn't* obvious.

**Watch for:** resenting the constant ("this feels stupid") — that's the rep working. Also: never delete an assertion or copy a computed actual into an expected to get green; that's faking the *test*, not the implementation.

### Variation 7 — Triangulation drill

**Test list:** V2 → V3's generalization, under one extra rule: **you may only generalize when a second test exists that the current fake fails** — and its argument values must be chosen so no shortcut survives (not `"2,2"` after `"1,3"`; both sum to 4).

**Goal:** experience the triangulation moment — the second test *pulling* generality out of the code — at least three times. Then, deliberately, find one step where triangulating would be ceremony (the pattern is obvious) and take *Obvious Implementation* instead, saying so out loud. Beck's own usage is the target: triangulate when genuinely unsure, not always.

**Watch for:** the second test that the fake accidentally passes — values too similar to force anything. If the bar stays green when you expected red, your test made no demand.

## Reflection prompt

After the time-box rings, write 2–4 sentences answering:

1. **What was the smallest step that taught you something?** Beck's claim is that step size is a dial; calibrating it is the skill. Where in this session did the dial setting feel right? Where did it feel wrong (too big, lost; too small, bored)?
2. **Did any refactor reveal design pressure?** A test that resisted, a structure that fought a clean change, a fixture that grew awkward — the resistance is the feedback. What did it tell you about the SUT?
3. *(Optional)* If you skipped the cycle anywhere ("just this once"), where, and what did you lose by skipping?

The answers are for you. Don't share them; don't grade them. The reflection IS the practice; everything before it was preparation.
