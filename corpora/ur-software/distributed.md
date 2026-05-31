# Ur-Software Corpus — Distributed Systems

Frozen reference for distributed systems reasoning. Pavel reasons FROM this, not about it. Updates are supersession events, not edits. Open surface marked [OPEN].

Three tiers:
- **Frozen**: invariants that have not moved in decades. Epistemic tag required: [theorem] (mathematically proven), [empirical] (well-observed, defeasible by counterevidence), [axiom] (staked-not-proven foundational commitment), [definition] (formal definition with provable properties).
- **Semi-liquid**: pattern wisdom with because. Fields: *because*, *canonical failure* (mechanistic — the causal path, not the symptom), *signals* (observable conditions suggesting this pattern applies), *cross-refs*.
- **Liquid**: specific technology instantiations. Not enumerated — agent generates from context.

Supersession spine: shows Aufhebung (preserve/negate/elevate), not linear progress. Negated patterns resurface when context changes.

---

## §1 Frozen invariants

1.1 CAP theorem `[theorem]` — In a distributed system, you can guarantee at most two of: Consistency (every read returns the most recent write), Availability (every request receives a response), Partition tolerance (the system continues operating despite network partition). Since network partitions are not optional in real networks, the operative choice is C or A under partition. Rules out: CA distributed systems at network scale; treating CAP as a three-way dial with continuous settings; using "eventual consistency" as a synonym for "available under partition."

1.2 PACELC `[theorem]` — Extension of CAP: when no partition exists, the system still trades off Latency vs Consistency. CAP describes partition behavior only; PACELC completes the picture. Rules out: treating CAP as the complete latency/consistency story; assuming consistency is only a partition-time concern.

1.3 Eight fallacies of distributed computing `[empirical]` — The network is reliable; latency is zero; bandwidth is infinite; the network is secure; topology doesn't change; there is one administrator; transport cost is zero; the network is homogeneous (Deutsch et al.). Rules out: optimistic network assumptions in system design; treating any fallacy as "usually true enough"; security assumptions in architectural reasoning (see Security note).

1.4 FLP impossibility `[theorem]` — No deterministic algorithm can guarantee consensus in an asynchronous distributed system if even one process can fail (Fischer, Lynch, Paterson, 1985). Rules out: "we'll just use consensus" as a reliability solution; deterministic consensus in async systems with any failure model.

1.5 Two generals problem `[theorem]` — Two parties communicating over an unreliable channel cannot achieve guaranteed agreement on a coordinated action. FLP is the formal generalization. Rules out: reliable commitment over unreliable transport without acknowledgment costs; assuming retries produce guaranteed delivery.

1.6 State/statelessness tension `[axiom]` — Stateful systems carry memory across requests; failure means state loss or expensive recovery. Stateless systems are resilient to failure but displace state to an external store that becomes the availability bottleneck. There is no free lunch: the choice is which failure mode to prefer. Rules out: "stateless is always better"; hiding state in caches while claiming statelessness; treating statelessness as an architectural purity goal.

---

## §2 Semi-liquid patterns

### Circuit breaker
*because:* Retrying against a degraded downstream amplifies load and cascades failure upstream. A circuit breaker short-circuits calls after a failure threshold, giving the downstream time to recover.
*canonical failure:* Threshold triggers on wrong error types (timeouts vs. application errors not distinguished); half-open state not meaningfully tested before fully closing; circuit state not surfaced to observability tooling, so open circuits are invisible until downstream SLA is missed.
*signals:* Downstream service with measured p99 latency spikes; retry storms visible in logs; downstream SLA materially lower than upstream SLA.

### Saga (distributed transactions)
*because:* Two-phase commit holds distributed locks across services for the full transaction duration; one slow or failed participant blocks all others. Sagas decompose a distributed transaction into a sequence of local transactions, each with a corresponding compensating operation that undoes it.
*canonical failure:* Compensating transactions not implemented for all steps — a partial failure leaves the system in an inconsistent state with no recovery path. Compensation logic written once and never tested in failure scenarios.
*signals:* A business operation spans multiple service boundaries; atomicity is required but 2PC lock contention or latency is unacceptable; services owned by different teams with independent deployment cycles.
*cross-refs:* [→ corpus_ursoftware_data — compensating transactions interact with ACID guarantees; understand the data tradeoffs before choosing saga scope]

### Idempotency
*because:* Distributed systems guarantee at-least-once delivery; duplicates will arrive. Idempotent operations produce the same result regardless of how many times they are executed.
*canonical failure:* Idempotency key scoped incorrectly — same operation from different contexts shares a key (false dedup) or same operation with different key is not deduped (no protection). Key chosen without analyzing the uniqueness domain.
*signals:* Consumer processes events from a queue or webhook; retry logic exists anywhere in the call chain; payment, inventory, or any state-mutation operation where duplicate execution has observable side effects.

### Backpressure
*because:* Unbounded queues absorb bursts temporarily but cause out-of-memory failures and unpredictable latency under sustained load. Backpressure signals producers to slow down before the buffer exhausts.
*canonical failure:* Backpressure implemented within one service but dropped at the seam with an adjacent service using a different queue implementation; producer treats the backpressure signal as an error to retry rather than a flow-control signal to honor.
*signals:* Measured throughput mismatch between producer and consumer; memory growth under load that doesn't stabilize; latency degradation that does not self-correct under steady traffic.

### Bulkhead
*because:* Shared thread pools and connection pools mean one overloaded downstream can exhaust shared resources and fail all downstreams. Bulkheads isolate resource pools by dependency.
*canonical failure:* Pool sizes set to defaults without traffic distribution analysis — the bulkhead for the critical path is undersized because it shares configuration defaults with low-traffic paths.
*signals:* Multiple downstream dependencies of significantly different criticality; one downstream with known reliability or latency variance; failure in one downstream currently impacting response time for unrelated requests.

---

## §3 Supersession spine

**Deployment unit evolution:** monolith → SOA → microservices → serverless/edge

Each step shows Aufhebung: the prior step's failure mode was preserved in history, negated as the active approach, and elevated into the successor. The unit of deployment got smaller at each step; the network boundary got more prominent; the eight fallacies hit harder. This is not linear progress — context determines which step is appropriate, and negated patterns resurge when context changes (modular monoliths are actively resurging as a response to microservices complexity at small-to-medium scale). Newer is not better.

---

## Security

Security concerns route through existing agent slots by phase — Pavel (substrate/dependency, ingestion), Daedalus + Urania (craft/lineage, review). [→ corpora/ur-software/security.md, logic.md §16.4]
