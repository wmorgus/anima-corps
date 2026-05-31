# Ur-Software Corpus — Application Architecture

Frozen reference for application architecture reasoning. Pavel reasons FROM this, not about it. Updates are supersession events, not edits. Open surface marked [OPEN].

Three tiers:
- **Frozen**: invariants that have not moved in decades. Epistemic tag required: [theorem] (mathematically proven), [empirical] (well-observed, defeasible by counterevidence), [axiom] (staked-not-proven foundational commitment), [definition] (formal definition with provable properties).
- **Semi-liquid**: pattern wisdom with because. Fields: *because*, *canonical failure* (mechanistic — the causal path, not the symptom), *signals* (observable conditions suggesting this pattern applies), *cross-refs*.
- **Liquid**: specific technology instantiations. Not enumerated — agent generates from context.

Supersession spine: shows Aufhebung (preserve/negate/elevate), not linear progress. Negated patterns resurface when context changes.

---

## §1 Frozen invariants

1.1 Separation of concerns `[axiom]` — A software component should have one reason to change. Mixing domain logic, persistence logic, and presentation logic in one component means changes to any layer force changes to all. *relaxes when:* prototype scope with no expected handoff, solo ownership with no other readers, throwaway code with an explicit expiration date named as such — relaxation must be named and scoped, not silent. Rules out: components that mix all three concerns; "it's simpler to keep it together" without naming the relaxation.

1.2 Dependency inversion principle `[axiom]` — High-level modules (domain logic) should not depend on low-level modules (infrastructure implementations); both should depend on abstractions. Rules out: application logic importing ORM or HTTP client classes directly; domain layer with infrastructure imports; framework-specific annotations in domain objects.

1.3 Ports and adapters (hexagonal architecture) `[axiom]` — The core domain has no knowledge of how it is accessed (HTTP, CLI, message queue) or what infrastructure it accesses (DB, email, payment provider). Ports are interfaces the domain defines; adapters implement them. *relaxes when:* single-surface application with no expected additional access patterns and infrastructure dependency has no realistic substitution pressure — the tradeoff trades future adaptability for present simplicity and must be named. Rules out: HTTP routing logic in domain services; domain models importing persistence classes; framework annotations in domain objects; "we'll add the port later."

1.4 Conway's Law `[empirical]` — Organizations produce systems whose communication structure mirrors their organizational communication structure. Designing architecture as if it's independent of how teams communicate produces systems that fight the org. Rules out: architecture design without org structure analysis; assuming clean cross-boundary interfaces without communication structures that support them; treating Conway's Law as a historical observation rather than a present constraint.
*cross-refs:* [→ corpus_ursoftware_distributed — org structure shapes where network boundaries fall; a team boundary is a latency and failure domain boundary, not just a component design boundary]

---

## §2 Semi-liquid patterns

### Layered n-tier architecture
*because:* Different layers change at different rates — UI changes fast, business rules at medium speed, DB schema slowly. Separating by rate of change isolates churn to the layer where it originates.
*canonical failure:* Layers become "lasagna" — each layer is a thin pass-through that adds indirection without enforcing a real boundary; business logic leaks into the UI layer because the intermediate layer has no behavior of its own; the separation is nominal.
*signals:* Multiple surfaces (web, mobile, API) need to share business logic; clear rate-of-change asymmetry exists between presentation and persistence; team boundaries align with layer boundaries.

### Domain-Driven Design (bounded contexts)
*because:* Complex domains require linguistic precision — "customer" means different things in billing, support, and fulfillment. A forced shared model causes semantic drift where every change to the model is contested across teams.
*canonical failure:* Anemic domain model — classes have domain names but no behavior; all business logic lives in service classes; the bounded context exists in naming conventions but not in actual encapsulation. The boundary is drawn but not enforced.
*signals:* Multiple teams arguing about the "correct" definition of a shared entity; model changes require cross-team coordination; high domain complexity with many rules, exceptions, and state transitions.

### CQRS (Command Query Responsibility Segregation)
*because:* Read and write operations have different scaling, latency, and consistency requirements. A single model optimized for writes is typically wrong for reads, and vice versa.
*canonical failure:* Applied where the asymmetry doesn't exist — a CRUD application with an even read/write ratio now has two models, two data stores, and synchronization complexity with no measurable benefit.
*signals:* Read/write ratio greater than 10:1; separate team ownership of query vs. command paths; read model requires denormalized projections that would degrade write performance.
*cross-refs:* [→ corpus_ursoftware_data — CQRS implies either read replicas or a separate read store; the data corpus contains the tradeoffs for both]

### Event-driven architecture
*because:* Publishers don't need to know their consumers; new consumers can be added without modifying the publisher; decoupling enables independent scaling and deployment of producer and consumer services.
*canonical failure:* Consumers proliferate without a registry; no single owner can trace a business transaction across handlers; schema evolution breaks consumers silently because there is no contract enforcement at the event boundary. The decoupling that was the feature becomes the liability.
*signals:* Multiple consumers need to react to the same state change; publisher and consumers have independent release cycles; fan-out to three or more consumers of the same event type.

---

## §3 Supersession spine

**Architectural unit evolution:** monolith → client/server → 3-tier → SOA → microservices → serverless/function

Each step shows Aufhebung: the prior step's failure mode was preserved in history, negated as the active approach, and elevated in the successor. This is not linear progress — modular monoliths are actively resurging as a response to microservices complexity at small-to-medium scale. Each step was a response to a specific scaling or organizational failure mode of the previous step; those failure modes do not appear uniformly across contexts. Newer is not better; context determines which step fits.

---

## Security

Security concerns route through existing agent slots by phase — Pavel (substrate/dependency, ingestion), Daedalus + Urania (craft/lineage, review). [→ corpora/ur-software/security.md, logic.md §16.4]
