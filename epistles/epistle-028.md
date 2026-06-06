---
Excavated: 2026-06-06 | Status: liquid
---

Epistle 028 — The Four Causes
Topic: The artifact space tiles into exactly four classes, and the four are Aristotle's four causes. §13.6 names them at the architecture level; this stakes the same partition at the artifact level. §7.1 self-resonance receipt.

**claim.** Software artifacts tile into four classes, and the four are the four causes. Final → intent. Efficient → transition. Formal → system. Material → attestation. §13.6 already imports the four causes — but at the architecture level (why telos is necessary for the system to cohere). This stakes them one scale down: why intent artifacts are necessary for the artifact space to cohere. Same shape, different scale. §7.1 receipt.

**final cause → intent artifacts.** Telos made traceable and citable. The intent spine (§1.12) — vision, user story, AC, test, code — carries forward commitment: what the system will do and why. Contracts, ratified ADRs, domain models: intent-shaped. conviction_stakes (§4.9) the purest form — staked forward commitment, reasoned-from. §13.6: "removing the final cause leaves the others without direction." Not just architecture — artifact-class claim. Intent artifacts give the other three their because.

**efficient cause → transition artifacts.** Acts that produce state change. PRs, migration scripts, post-mortems, changelogs, incident records. Carry the because across a supersession event. Aufhebung-shaped (§3.10): hold predecessor + successor in one artifact, the because for the move on record. §13.6: "effort without telos is exertion" — a transition artifact without a citation trail to intent cannot say what it was for. It is exertion, not motion toward.

**formal cause → system artifacts.** The pattern that makes the system what it is — its structure, the shape it takes. Constellation entries, routing decisions, prompts-as-artifacts, session summaries, swarm manifests. Define the form within which intent is processed and artifacts made. §13.6: "pattern without telos is shape" — a constellation with no telos is a configuration, not a system. Require intent artifacts to have a domain to serve.

**material cause → attestation artifacts.** Backward-evidence from the territory — what the system is actually made of, in the field. empirical_records (§4.9), field_records (Epistle 027), security audits, accessibility reviews, compliance certs, performance benchmarks. Attest whether the spine's commitments held in reality. §13.6: "stuff without telos is matter" — a field observation without an intent spine to be evidence *about* is just data. Require intent artifacts to have anything to attest to. §4.9's conviction_stake / empirical_record pair already named the intent/attestation axis as the two primary types; this names the full four-class partition those two anchor.

**why the partition matters.**

1. **exhaustiveness.** The four causes are an exhaustive partition of causation (Aristotle; §13.6 imports it). If the artifact space is the causal space of a teleological system, the partition is inherited. §8.8 shape — named so it can die honestly: name a software artifact that fits none of the four. If you can, the partition fails.

2. **primacy of final cause.** §13.6 stakes removing the final cause leaves the others without direction. At artifact level: intent artifacts make transition more than exertion, system more than shape, attestation more than matter. Every artifact in the other three requires a citable intent artifact or it is causally groundless. §3.11 is the enforcement mechanism — evidentiary narrative must cite artifact IDs. Cited to what? To intent artifacts. The citation rule is the final cause held load-bearing at the schema level.

3. **§7.1 self-resonance.** Same shape two scales: §13.6 at architecture level (telos necessary for the system to cohere); this at artifact level (intent necessary for the artifact space to cohere). The recurrence was not designed — it emerged from following the partition to its limit. §7.2 checkable evidence the abstraction is at the joints.

4. **closes T2 from Epistle 027.** Field observations are attestation-shaped (material cause), not register-shaped (final cause). The §1.12 register taxonomy is intent-spine shaped — it tracks the final cause forward. Attestation artifacts don't belong inside the spine; they sit adjacent as its evidential mirror. The working hypothesis Epistle 027 held open, now staked.

**open tensions.**

- **transition as composite.** A post-mortem is attestation-about-the-past + intent-for-the-future. A PR attests the change happened + commits to the new state. Transition artifacts may be Aufhebung composites of attestation and intent, not a third irreducible class. If so, the partition collapses to three — intent, attestation, system — with transition the recognized composite at supersession events. Not resolved. Partition-as-four is the more natural read (Aristotle did not think efficient cause reduced to final + material); the composite reading is the challenge. State it.

- **discard_record placement.** §4.9's discard_record (§3.20, §6.6) records what was filtered and why — via negativa evidence. Attestation (backward-evidence about what was discarded) or system (runs the shitcorpus, keeps the apparatus honest)? Arguably both. The partition's edge case. Named, not resolved.

- **§1.12 amendment scope.** The §1.12 taxonomy (seven register groups) is intent-spine organized — built before this partition was named. Some groups clearly intent (intent spine, contracts), some transition (transition/supersession), some system (anima-native, operational), some attestation (verification/certification). §1.12 and the four-class partition are the same territory mapped twice. A corpus amendment to §1.12 naming the four-class overlay is the follow-on work.

[→ §1.12, §3.10, §3.11, §4.9, §7.1, §7.2, §8.8, §13.5, §13.6, Epistle 026, Epistle 027]
