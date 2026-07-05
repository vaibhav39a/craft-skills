# Symptoms of Complexity

Source: John Ousterhout, *A Philosophy of Software Design* (2018) — provenance: web-sourced (https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lecture.php?topic=complexity, https://web.stanford.edu/~ouster/cgi-bin/cs190-spring16/lecture.php?topic=complexity)

## When it applies

- A conceptually simple change is fanning out across many files
- Making a change safely requires holding too much of the system in your head
- Nobody can say where the needed knowledge lives — or whether it's relevant

## The rule

Complexity is anything about a system's structure that makes it hard to work on — *apparent* complexity as developers experience it, not size or feature count. Three symptoms name it: **change amplification** (a simple change needs many modifications), **cognitive load** (too much to know to change it correctly), **unknown unknowns** (the needed information exists but isn't findable). Keep symptoms distinct from the two root *causes*: **dependencies** and **obscurity** (the opposite of obscure: a developer's first guess about behavior is right). Complexity is incremental — thousands of small dependencies and obscurities — so the stance is zero tolerance: sweat the small stuff.

## Anti-patterns

- Treating a symptom (slow changes) without naming which one it is — each symptom points at different dependencies or obscurities
- Tolerating "just this one" small obscurity — the whole mechanism of complexity is accumulation

## In the agentic era (observed 2026-07)

Agents mask cognitive load instead of removing it: they hold the system in *their* context, the change lands, and the human's understanding never had to exist — comprehension debt wearing the costume of productivity. Meanwhile agents produce complexity's increments at machine speed, so zero tolerance now applies to reviewing diffs: each small new dependency or obscurity in generated code is a unit of future suffering. When a "simple" request keeps touching many files, name change amplification — that's the design talking, not the task.
