# Deep Modules

Source: John Ousterhout, *A Philosophy of Software Design* (2018) — provenance: web-sourced (https://web.stanford.edu/~ouster/cgi-bin/cs190-spring16/lecture.php?topic=modularDesign, https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lecture.php?topic=modularDesign)

## When it applies

- A module's interface is growing nearly as large as what it does
- A design is sprouting many small classes, each adding the least possible functionality
- An interface decision is trading implementation convenience against caller simplicity

## The rule

Maximize functionality relative to interface complexity: a deep module offers lots of functionality behind a simple interface and hides lots of information (Unix file I/O is the canonical example). The interface is everything a caller must know — including side effects, not just signatures. It's more important for a class to have a simple interface than a simple implementation. On size, Ousterhout is explicit that size isn't the metric — depth is. Make modules "somewhat generic": an interface usable beyond today's needs is usually the deeper one.

## Anti-patterns

- **Shallow module** — little functionality relative to its interface; in the extreme, invoking the method costs almost as much as retyping it inline
- **Classitis** — too many classes, each adding the least possible functionality; every class taxes the system with its interface even when each is individually simple

## In the agentic era (observed 2026-07)

Agents are classitis machines: asked to scaffold a feature, they cheerfully generate constellations of small pass-through classes, and each one *looks* clean in isolation. Interface design is the judgment surface the human must hold — when a scaffold sprouts tiny classes or a module's interface rivals its implementation, name it and ask what single deeper interface would absorb them. Reviewing for depth (what does the caller have to know?) is a sharper agent-output filter than reviewing for style.
