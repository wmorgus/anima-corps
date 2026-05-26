# Ur-Software Corpus — Data

Frozen reference for data storage and modeling reasoning. Pavel reasons FROM this, not about it. Updates are supersession events, not edits. Open surface marked [OPEN].

Three tiers:
- **Frozen**: invariants that have not moved in decades. Epistemic tag required: [theorem] (mathematically proven), [empirical] (well-observed, defeasible by counterevidence), [axiom] (staked-not-proven foundational commitment), [definition] (formal definition with provable properties).
- **Semi-liquid**: pattern wisdom with because. Fields: *because*, *canonical failure* (mechanistic — the causal path, not the symptom), *signals* (observable conditions suggesting this pattern applies), *cross-refs*.
- **Liquid**: specific technology instantiations. Not enumerated — agent generates from context.

Supersession spine: shows Aufhebung (preserve/negate/elevate), not linear progress. Negated patterns resurface when context changes.

---

## §1 Frozen invariants

1.1 Normalization (1NF/2NF/3NF) `[definition]` — 1NF: atomic values, no repeating groups. 2NF: no partial dependency on a composite primary key (every non-key attribute depends on the whole key). 3NF: no transitive dependency (non-key attributes depend only on the key, not on other non-key attributes). Normal forms are formal definitions; the theorems are about what anomaly-elimination properties schemas in those forms have. Rules out: denormalization as default; treating normalization as a style preference; "we'll normalize later"; conflating the definitions with the proofs about their properties.

1.2 ACID vs BASE `[axiom]` — ACID (Atomicity, Consistency, Isolation, Durability): relational database guarantee — transactions complete fully or not at all, committed data persists, concurrent transactions do not observe each other's intermediate state. BASE (Basically Available, Soft state, Eventually consistent): NoSQL tradeoff — availability prioritized over consistency, replicas may diverge temporarily. These are not synonyms with different names; they are different contracts with different failure modes. Rules out: choosing NoSQL for performance without acknowledging the consistency contract change; assuming BASE systems are "ACID but faster"; treating eventual consistency as a timing detail rather than a consistency model.

1.3 Object-relational impedance mismatch `[empirical]` — Objects have identity, graphs, and inheritance; relations have rows, columns, and foreign keys. The two models are structurally incompatible. Every ORM is a negotiation with this mismatch, not a resolution of it. Rules out: treating ORM as "solved" object-relational mapping; assuming the mismatch is an implementation detail; expecting ORM to make relational data feel naturally object-oriented without cost.

1.4 Write-ahead logging `[theorem]` — Durability requires that a write is persisted to a log before the commit is acknowledged; crash recovery replays the log to restore committed state. An in-memory commit without WAL cannot survive a crash with durability guarantees. Rules out: treating in-memory commit as durable; "we'll add durability later"; caching layers that claim durability without WAL semantics.

1.5 Data locality `[axiom]` — The cost of a join is proportional to the data moved across the join boundary, not the data read. Joins that cross storage nodes, network boundaries, or large page ranges are expensive by the nature of the operation, not by implementation quality. Rules out: treating joins as free operations; "we'll optimize later" when joins are architectural decisions; assuming the query planner eliminates join cost at scale.

1.6 Index as tradeoff `[axiom]` — Every index is a write-time tax paid for read-time performance. Indexes degrade write throughput, occupy storage, and must be maintained on every mutation. There is no read optimization via index that does not cost at write time. Rules out: adding indexes reactively without accounting for write degradation; treating index count as neutral; "indexes are free."

---

## §2 Semi-liquid patterns

### Denormalization as deliberate choice
*because:* Normalization eliminates redundancy at the cost of joins. When read performance dominates and join cost is the measured bottleneck, controlled denormalization trades write complexity for read speed.
*canonical failure:* Writes now update multiple denormalized copies; one update path fails or is missed; data becomes inconsistent with no automated detection. The consistency burden is displaced from the schema to the application layer, where it is harder to enforce.
*signals:* Read/write ratio heavily skewed toward reads; join cost measured as the bottleneck in profiling; read latency SLA cannot be met with a normalized schema under production load.

### Sharding (horizontal partitioning)
*because:* Single-node write throughput has a hardware ceiling. Sharding distributes writes across nodes by partitioning the key space.
*canonical failure:* Hot shard from uneven key distribution — a partition key chosen for convenience (e.g., created_at date, sequential ID) concentrates writes on the newest or highest shard while older shards sit idle. The shard that matters most is the one that's overwhelmed.
*signals:* Single primary write throughput approaching hardware ceiling; dataset size exceeding single-node storage capacity; write latency degrading under load with no other measured bottleneck.

### Read replicas
*because:* Read-heavy workloads can be offloaded from the primary, reducing read latency and freeing primary capacity for writes.
*canonical failure:* Reading own writes from a replica that hasn't caught up — a write succeeds on primary, a subsequent read from the replica returns pre-write state, creating a consistency violation invisible to the writer.
*signals:* Read/write ratio greater than 5:1; read latency degrading while write latency is acceptable; read queries measurably impacting write throughput on the primary.
*cross-refs:* [→ corpus_ursoftware_application — CQRS implies either read replicas or a separate read store; the architectural decision precedes the data decision]

### Caching layer
*because:* Most reads in production systems are repeat reads. A cache serves repeat reads from memory, reducing database load and latency by orders of magnitude.
*canonical failure:* Cache stampede — a popular key expires; all concurrent requestors miss simultaneously and send requests directly to the database; the resulting spike causes latency that triggers more cache misses; positive feedback loop that can take down the database.
*signals:* High repeat read ratio on expensive queries; database CPU driven primarily by reads; read latency SLA cannot be met at the database directly under production traffic.

### Materialized views
*because:* Expensive aggregation queries run repeatedly against large tables. Precomputing and storing the result amortizes the computation cost across reads.
*canonical failure:* Stale materialized view — the refresh is not triggered on source data change, or refresh lag is longer than the staleness tolerance of the consumer. The consumer reads precomputed data that no longer reflects current state.
*signals:* Same expensive aggregation query running frequently against large tables; query time dominates a report generation or dashboard path; source data changes infrequently relative to read demand.

---

## §3 Supersession spine

Storage paradigm evolution: relational → document → key-value → column-family → graph → vector

Each step shows Aufhebung: the prior paradigm's access asymmetry limitation was preserved in history, negated as the sole answer, and elevated in a new paradigm optimized for a specific access pattern. Relational databases remain correct for most transactional workloads; the spine represents the emergence of access patterns (document structure, high-cardinality key lookup, graph traversal, semantic similarity) that relational could not serve efficiently — not a replacement sequence. Newer is not better; the access pattern and consistency requirements determine the appropriate paradigm.

---

## Security

No security corpus exists. Agents operating without a security corpus must flag security-relevant data decisions (encryption at rest, access control, PII handling) for human review rather than reasoning from silence.
