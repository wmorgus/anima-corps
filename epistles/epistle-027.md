---
Excavated: 2026-06-03 | Status: liquid
---

Epistle 027 — The Minimum Viable Telos
Topic: The least a system needs to cross from "we wrote down our goals" into teleological software. The reductive floor under §1.11.

§1.11 stakes teleological software as thesis term and names the full committed stack — append-only store, ratification cycle, citation-as-schema, supersession. Names everything that stack *requires when committed to as infrastructure*. Never isolates the minimum. This epistle stakes that floor. Downstream of epistle-026: the chef does not abandon the kitchen to know what a dish minimally is.

**MVT floor — three structural requirements.** Software is teleological at minimum iff all three:

(a) **Telos held externally to the executor.** Not in the model weights. Not in the agent's prompt-as-intention. Held in a place the executor reads from but does not author. This is §3.3's externality requirement read at the telos layer — the validator external to the thing validated, now the *end* external to the thing pursuing it. If the executor holds its own telos, it ratifies its own purpose. Self-attestation at the goal level.

(b) **Telos readable by the executor.** Structured and navigable — not prose intentions the executor cannot traverse. A goals doc in paragraphs the agent never parses fails (b) even if it passes (a). Novel constraint: the corpus stakes structure for citation and lineage but has not named a *readability* requirement at the telos level. MVT names it. "Structured enough to navigate" is the bar.

(c) **A revision path.** Documented mechanism for flagging when recipe diverges from real end — when the written telos and the actual end pursued come apart. §3.10's supersession reduced to minimum surface. Not the full Aufhebung cycle; the *path* by which divergence gets surfaced and the telos can be superseded rather than silently drifted from.

Everything else — full ratification cycle, hub-and-spoke topology, citation-as-schema — is operational hardening. Earns its weight at scale, not at the floor.

**Artifact collapse at small scale.** The telos doc, the claim registry, the revision protocol may collapse into one document. Three requirements, not three files. What separates "we wrote down our goals" from MVT is structure + revision path — not artifact count. This rules out the impersonator §1.11 cannot rule out alone: the team with a goals doc that *believes* it has teleological software. The discriminator is (c), the revision path. Not document boundaries. The team with three pristine artifacts and no way to flag divergence is further from MVT than the team with one document that can be flagged and superseded. Via-negativa floor of the full multi-artifact architecture.

**Append-only as structural enforcement of the revision path.** Minimum practical store: one append-only log. Two entry classes — recipe entries (human-ratified telos and supersessions) and flag entries (executor-surfaced divergences). Overwriting is defection. Supersession is an append. This extends §4.2 — append-only as the structural condition under which ratification can mean anything — down to the two-entry-class minimum. Names *which* discipline append-only enforces at the floor: the revision path specifically (c), not ratification in general. Mutable store → the flag and the recipe it contradicts cannot coexist → divergence is erased instead of surfaced → (c) fails structurally.

**Open — does (b) pre-decide §6a.10?** (b) requires telos "structured enough to navigate" but names no retrieval primitive. §6a.10 leaves pull-vs-push open at agent-init. (b) seems to require readability *without* specifying how context reaches the executor. Does MVT's readability requirement pre-decide §6a.10, or sit above it? Reading: (b) is silent on primitive — it demands the telos be navigable, not that the executor pull rather than receive push. Pull and push both satisfy (b) if the delivered telos is structured. So (b) sits above §6a.10. But §6a.10 notes pull respects externality (§3.3) at every invocation and push collapses it — and MVT's (a) is §3.3 at the telos layer. So if push collapses externality, push may quietly fail (a) even while satisfying (b). Genuinely open whether (b) and (a) together force the §6a.10 choice that §6a.10 itself leaves open. Name, don't resolve.
