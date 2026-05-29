---
Excavated: 2026-05-29 | Status: vapor
---

Epistle 018 — Instantiation has no home in the frozen tier
Topic: Frozen corpora hold timeless invariants. Time-sensitive instantiations (CVE landscape, framework versions, EOL, regulatory state) have no architectural home. Stake the gap. Resolve the mechanism (retrieval-target model, security.md §4 generalized). Leave the per-domain targets open.

The gap. Frozen tier holds invariants — correct, stable, unmoved in decades (security.md §1; logic.md §2.1). But some knowledge is inherently timed: a CVE against a version, a library at EOL *right now*, the current OWASP edition, this framework deprecated this quarter. Cannot freeze a CVE. The corpus has nowhere to put it.

The cop-out. Four ur-software corpora (data, concurrency, application, distributed) defer with the same line: "Liquid: specific technology instantiations. Not enumerated — agent generates from context." Agent generates from context → agent uses training data → stale, and not the corpus. The deferral names a tier and then fills it with the model's memory. A liquid tier whose contents are the model's training cutoff is not liquid. It is frozen at a date nobody chose and nobody can read.

The distinction the corpus doesn't make cleanly. Two different things wear one word:
- **Invariant** — what makes a good dependency decision. Lock files authoritative; exposure determined by what's pinned not what's latest (security.md §2). Timeless. Belongs frozen.
- **Instantiation** — *this* library at *this* version is EOL today. Expires. Belongs nowhere, currently.
The frozen tier holds the former. The latter is homeless. The four corpora collapse the distinction into "generate from context" and lose it.

Argus was the symptom. Argus queued as security agent → because CVE/OWASP/NIST/KEV are live references and the corpus couldn't hold them, so something had to fetch them. security.md §4 already partially fixed this: its liquid tier is *retrieval targets*, not generated specifics — "the agent looks specifics up from authoritative external sources at decision time" (§4, line 110), explicitly contrasting itself against the other corpora's generate-from-context liquid. So security solved its own instance with an agent + retrieval contract. The right fix isn't one more agent per timed domain — it's the §4 *pattern* (retrieval targets named in the corpus, fetched at decision time) generalized across all domains. Argus is the symptom; the homeless tier was the disease. security.md §4 is not just one local cure — it is the architecture, demonstrated once. The remaining work is propagating it, not inventing it.

The mechanism — resolved. Three candidates; option 3 wins.
1. **Timed-expiry annotations** on liquid claims — expiration dates, re-verification intervals, a curator step. Ruled out: puts expiry ON the corpus claim. That is decay — a stake going stale — forbidden by §3.9 ("TTLs as primitive; time-bounded expiry; stigmergic decay") and §3.10 ("Rules out: erasure; expiry; edit-in-place").
2. **Maintained current-state document** — separate from frozen, owned, re-issued on cadence. Ruled out: a maintained doc is a second corpus. It also goes stale, also needs updating. Same problem one level up — the homelessness is relocated, not dissolved.
3. **Live query at reasoning time** — name retrieval targets, fetch at decision time, cite source + timestamp. The security.md §4 model. Wins. The corpus entry names *where to look*; it does not hold the timed fact. No expiry on the claim. The freshness lives in the external source.

The §3.9 collision — dissolved, not open. §3.9 forbids decay: a *stake going stale*, a claim with a TTL. Option 3 puts no TTL on the corpus claim. The entry "look up CVEs at NVD/KEV at decision time" is itself a frozen invariant — the retrieval target doesn't change. What expires is the fetched data, at the source, outside the corpus. Retrieval-at-decision-time ≠ decay. §3.9/§3.10 stay intact. The earlier residual ("corpus rules out expiry; problem needs expiry") was confused: the problem never needed expiry on the *claim* — only on the *fetched content*, which the corpus never holds.

The cop-out was the wrong instance of the right tier. "Agent generates from context" confused two acts: agent uses training data (stale, unread, frozen at a date nobody chose) vs. agent queries live sources (fresh, cited, timestamped). The fix is not a new mechanism — security.md §4 already built it correctly. The fix is generalization: replace "Not enumerated — agent generates from context" in all four ur-software corpora (data, concurrency, application, distributed) with explicit retrieval targets per domain. The corpus entry stays frozen (the target doesn't move); the fetched content is live (it moves at the source).

What's still open — the targets, not the architecture. The architecture is resolved: retrieval-target model, generalized from security.md §4. The content is not. What are the correct authoritative sources per domain? — data (dependency registries, ORM/driver deprecation trackers, DB-engine EOL feeds?); concurrency (runtime/scheduler changelog feeds?); application (framework advisory feeds, deprecation trackers?); distributed (protocol/spec version feeds, managed-service EOL notices?). Security had clean targets — NVD, GHAD, KEV, OWASP, NIST crypto. The other four do not yet have named equivalents. Naming them per domain is the remaining work. [→ logic.md §2.1, §3.9, §3.10; security.md §4]
