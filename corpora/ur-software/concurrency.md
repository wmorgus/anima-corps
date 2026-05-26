# Ur-Software Corpus — Concurrency

Frozen reference for concurrency reasoning. Pavel reasons FROM this, not about it. Updates are supersession events, not edits. Open surface marked [OPEN].

Three tiers:
- **Frozen**: invariants that have not moved in decades. Epistemic tag required: [theorem] (mathematically proven), [empirical] (well-observed, defeasible by counterevidence), [axiom] (staked-not-proven foundational commitment), [definition] (formal definition with provable properties).
- **Semi-liquid**: pattern wisdom with because. Fields: *because*, *canonical failure* (mechanistic — the causal path, not the symptom), *signals* (observable conditions suggesting this pattern applies).
- **Liquid**: specific technology instantiations. Not enumerated — agent generates from context.

Relationship to distributed corpus: concurrency and distribution share happens-before and some failure modes. They are distinct reasoning surfaces: distributed = across processes/machines, failure through network; concurrent = within a process, failure through scheduling. [→ corpus_ursoftware_distributed]

---

## §1 Frozen invariants

1.1 Happens-before (Lamport) `[theorem]` — Event A happens-before event B if: A and B are in the same process and A precedes B in execution order; A sends a message and B receives it; there exists C such that A happens-before C and C happens-before B. Happens-before is a partial order — not all pairs of events are comparable; events that are not ordered by happens-before are concurrent with no defined sequence. Rules out: assuming all events have a meaningful global ordering; treating concurrent events as having a defined sequence; reasoning about distributed event order without explicit synchronization.

1.2 Memory visibility / data races `[theorem]` — Without explicit synchronization, there is no guarantee that a write in one thread is visible to a read in another thread. The CPU and compiler are permitted to reorder instructions and cache writes locally. A data race — concurrent unsynchronized access to the same memory location where at least one access is a write — produces undefined behavior under all major memory models. Rules out: assuming shared memory is coherent without synchronization; "it works in practice" reasoning about unsynchronized access; treating data races as performance problems rather than correctness violations.

1.3 Language memory models `[axiom]` — Hardware reordering is the mechanism; language memory models (Java Memory Model, C++11 memory model) are the agent-facing contract. `volatile`, `atomic`, `synchronized`, and memory ordering annotations have semantics defined by the language model, not by hardware. The same hardware instruction sequence may have different visibility guarantees under different language models. An agent generating concurrent code must reason against the language memory model of the target language, not against hardware behavior directly. Rules out: reasoning about memory visibility from hardware behavior alone; assuming `volatile` means the same thing across languages; generating concurrent code without specifying the memory model; treating language-level concurrency primitives as thin hardware wrappers.

1.4 Lock granularity tradeoff `[axiom]` — Coarse-grained locks are simple but serialize all access to a protected region and reduce throughput. Fine-grained locks increase throughput under contention but increase complexity and deadlock risk. There is no granularity that is universally correct — the tradeoff is determined by measured contention patterns. Rules out: defaulting to one strategy without analyzing contention; assuming fine-grained is always better; assuming coarse-grained is always safe.

1.5 Deadlock conditions (Coffman 1971) `[theorem]` — Deadlock requires all four conditions simultaneously: mutual exclusion (resource held exclusively by one thread), hold-and-wait (thread holds one resource while waiting for another), no preemption (resources cannot be forcibly taken from a thread), circular wait (cycle exists in the resource-wait graph). Eliminating any one condition prevents deadlock. Rules out: deadlock prevention strategies that do not break at least one condition; assuming deadlock is a rare edge case in systems with multiple lock acquisition sites.

1.6 TOCTOU (Time of Check to Time of Use) `[theorem]` — A race condition where the system state changes between a check and the action that depends on that check result. The check result is stale by the time it is used, and the action proceeds on a false premise. Rules out: assuming check-then-act sequences are atomic without explicit synchronization; filesystem operations based on prior existence checks; any conditional action based on a non-atomic read in a concurrent context.

1.7 ABA problem `[theorem]` — In compare-and-swap operations: a value is read as A by thread 1; thread 2 changes it to B and then back to A; thread 1's CAS succeeds because it observes A, but the intermediate state change is not detected. The CAS correctness assumption — "if the value is still A, nothing relevant changed" — is violated. Rules out: using CAS for operations that require detecting intermediate state changes; assuming CAS is a general solution to linearizability; tagged-pointer approaches where tag space is exhausted.

1.8 False sharing `[empirical]` — Unrelated data fields on the same CPU cache line cause cache invalidation across threads on every write to either field, even though neither thread is accessing the other's data. Manifests as unexpected throughput degradation under concurrency with no visible lock contention. Rules out: treating struct and class field layout as performance-neutral in concurrent contexts; assuming cache line boundaries are a hardware implementation detail irrelevant to software design.

1.9 Memory ordering violations `[theorem]` — Without explicit memory barriers or ordering annotations, the compiler and CPU are permitted to reorder writes and reads relative to each other. A write made visible to one thread may not be visible to another in the order it was made. Intermittent failures that disappear under debugging or reduced optimization levels are the canonical signal. Rules out: assuming write ordering is preserved without explicit synchronization; treating memory ordering as a hardware quirk rather than a programming model constraint; assuming sequential consistency as the default.

---

## §2 Semi-liquid patterns

### Optimistic concurrency control
*because:* Pessimistic locking acquires a lock before reading, serializing all access — under low contention, most lock acquisitions are uncontested overhead. Optimistic concurrency reads without locking and detects conflicts at write time via version check or compare-and-swap.
*canonical failure:* High conflict rate — transactions repeatedly fail and retry, producing more total work than pessimistic locking would have. Optimistic concurrency degrades exactly where contention is highest, which is often where the critical path is.
*signals:* Read-heavy workload with measured low write conflict probability; contention measurably low in profiling; latency-sensitive operations where lock acquisition overhead is a significant fraction of total latency.

### Actor model
*because:* Shared mutable state requires synchronization that is difficult to reason about and compose. Actors encapsulate state and communicate exclusively through message passing — no shared state, no locks needed within an actor.
*canonical failure:* Mailbox overflow — an actor receives messages faster than it processes them; the mailbox grows unbounded; OOM or unbounded latency results. Actors do not eliminate backpressure; they relocate it to the mailbox boundary, where it must still be designed.
*signals:* High concurrency with complex shared state where lock reasoning is error-prone; lock contention measured as the bottleneck; work decomposes naturally into isolated stateful entities.

### Immutability as concurrency strategy
*because:* Immutable data can be safely shared across threads without synchronization — there are no writes after construction, so reads never race with writes.
*canonical failure:* Defensive copying at mutable boundaries — code claims immutability but accepts mutable arguments and copies them at construction; the copy operation itself is unsynchronized if the source is mutable, making the "immutable" object's construction a race condition.
*signals:* Frequently read, rarely mutated data shared across threads; functional-style processing pipeline; data that is logically a value (configuration snapshots, messages, domain events).

### Lock-free data structures
*because:* Under high contention, lock acquisition overhead and thread blocking dominate; lock-free structures use compare-and-swap to achieve thread safety without mutual exclusion, allowing progress even when other threads are delayed.
*canonical failure:* CAS retry loop spins indefinitely under adversarial scheduling (livelock); progress guarantees are weaker than lock-based structures in worst-case scenarios — lock-free means at least one thread makes progress, not that all threads do.
*signals:* Measured lock contention on a specific data structure in profiling; structure is a hot path accessed simultaneously by many threads; throughput bottleneck is at the data structure level, not at business logic.

---

## Security

No security corpus exists. Agents operating without a security corpus must flag security-relevant concurrency decisions (race conditions in authentication paths, timing attacks) for human review rather than reasoning from silence.
