---
Excavated: 2026-05-29 | Status: vapor
---

Epistle 018 — Instantiation has no home in the frozen tier
Topic: Frozen corpora hold timeless invariants. Time-sensitive instantiations (CVE landscape, framework versions, EOL, regulatory state) have no architectural home. Stake the gap. Defer the mechanism.

The gap. Frozen tier holds invariants — correct, stable, unmoved in decades (security.md §1; logic.md §2.1). But some knowledge is inherently timed: a CVE against a version, a library at EOL *right now*, the current OWASP edition, this framework deprecated this quarter. Cannot freeze a CVE. The corpus has nowhere to put it.

The cop-out. Four ur-software corpora (data, concurrency, application, distributed) defer with the same line: "Liquid: specific technology instantiations. Not enumerated — agent generates from context." Agent generates from context → agent uses training data → stale, and not the corpus. The deferral names a tier and then fills it with the model's memory. A liquid tier whose contents are the model's training cutoff is not liquid. It is frozen at a date nobody chose and nobody can read.

The distinction the corpus doesn't make cleanly. Two different things wear one word:
- **Invariant** — what makes a good dependency decision. Lock files authoritative; exposure determined by what's pinned not what's latest (security.md §2). Timeless. Belongs frozen.
- **Instantiation** — *this* library at *this* version is EOL today. Expires. Belongs nowhere, currently.
The frozen tier holds the former. The latter is homeless. The four corpora collapse the distinction into "generate from context" and lose it.

Argus was the symptom. Argus queued as security agent → because CVE/OWASP/NIST/KEV are live references and the corpus couldn't hold them, so something had to fetch them. security.md §4 already partially fixed this: its liquid tier is *retrieval targets*, not generated specifics — "the agent looks specifics up from authoritative external sources at decision time" (§4, line 110), explicitly contrasting itself against the other corpora's generate-from-context liquid. So security solved its own instance with an agent + retrieval contract. But the right fix isn't one more agent per timed domain. It's a corpus architecture that can hold timed-expiry instantiation across all domains. Argus is the symptom; the homeless tier is the disease. security.md §4 is one local cure, not the architecture.

The mechanism — held open. Candidates, none chosen:
1. **Timed-expiry annotations** on liquid claims — explicit expiration dates, re-verification intervals, a curator step.
2. **Maintained current-state document** — separate from frozen, owned, re-issued on cadence.
3. **Live query at reasoning time** — the security.md §4 model generalized: name retrieval targets, fetch at decision time, cite source + timestamp.

Cannot decide yet. Genuinely open.

Tension to hold, not resolve. Option 1 collides head-on with logic.md §3.9/§3.10. §3.9: "TTLs as primitive; time-bounded expiry; stigmergic decay" — explicitly ruled out; decay is "wrong in a hub-and-spoke topology." §3.10: supersession is Aufhebung, not expiry — "Rules out: erasure; expiry; edit-in-place." So timed-expiry annotations are forbidden by the conviction corpus *as a primitive*. Either (a) instantiation expiry is a different thing than the decay §3.9 rules out — a fact going stale is not a stake decaying — or (b) the homeless tier needs a mechanism that isn't expiry at all, and §3.9/§3.10 are the reason the cop-out exists rather than a real liquid tier. Don't know which. Flag: resolving this likely decides the mechanism. The corpus rules out expiry; the problem looks like it needs expiry. That residual is the epistle.

What's deferred. No proposed schema. No curator role. No decision on whether the four ur-software corpora get rewritten to the security.md §4 retrieval-target model or get something new. Stub stakes the gap and the §3.9 collision. Resolution is later work. [→ logic.md §2.1, §3.9, §3.10; security.md §4]
