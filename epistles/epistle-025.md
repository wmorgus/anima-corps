---
Excavated: 2026-06-01 | Status: liquid
---

Epistle 025 — Four Causes, Four Debts
Topic: The four debt primitives of Epistle 015 map one-to-one onto Aristotle's four causes. Each primitive is a cause-failure. The mapping grounds exhaustiveness harder than 015 did, and predicts causal interaction between debt types.

**claim.** The four primitives (015) are the four causes (§13.6) read as failures. Final → spec. Efficient → epistemic. Material → substrate. Formal → craft. Not analogy — identity of structure. A software artifact has exactly four causes; debt is what you measure when one is broken.

**the mapping.**
- Final cause / telos → **spec debt.** Code no longer serves its purpose. The telos bond is broken. The artifact runs but toward the wrong end (§1.7 shifted referent, §8.1).
- Efficient cause / the because, what brought it about → **epistemic debt.** Nobody knows why it was made this way. The efficient cause is unrecoverable (§1.7 missing because, §8.2).
- Material cause / what it's embedded in → **substrate debt.** The material moved. The world the code was coherent against shifted (§1.7 moved substrate, §8.4).
- Formal cause / intrinsic shape → **craft debt.** The artifact is ill-shaped: coupling, lost cohesion, accidental complexity. The formal cause is degraded (015 craft leg).

Note: 015's craft was "not an alignment failure — a quality failure." The cause frame absorbs this cleanly. Formal cause is the one cause intrinsic to the artifact; the other three are relations to something outside it (end, maker, world). 015's relational/intrinsic cut is the same cut as relational-cause / formal-cause. The mapping recovers 015's own seam, not despite it but as it.

**exhaustiveness — stronger than 015.** 015 argued from "a problem is relational or intrinsic, and the relational ones are enumerated" (the partition principle). Good but informal — the enumeration of three relations was justified by §1.12's spine, an internal architectural fact. The cause frame grounds it externally: the four causes are a complete account of causation for any made thing. Aristotle built them to be exhaustive. If every cause-failure maps to exactly one primitive, the primitives are exhaustive — not over Mnemo's surface, not over Anima's spine, but over *anything that can fail in a made thing*. You cannot have a software problem that is not a cause-failure. Either the partition inherits a 2400-year-old exhaustiveness claim, or naming a software problem that is no cause's failure breaks both at once. 015's falsifiability condition and this one are now the same condition.

**via negativa formulation.** Complete artifact = all four causes intact: well-formed, serves its purpose, its making traceable, embedded in a live world. No debt. Debt = cause-failure. Name which cause is broken — you have named the debt type. The taxonomy is not a list to memorize; it is "which of the four is missing." (Same move as §13.6 ran in one direction — remove final cause, the rest lose direction — generalized to all four.)

**telos doc / debt decomposition are dual.** A telos doc structured by the four causes shows all four present and intact. A debt decomposition shows which are missing or broken. Same framework, opposite orientation — one a positive census of causes, the other a negative one. The via negativa that builds the telos artifact (§1.11, §1.12) is the via negativa that builds the debt taxonomy. They are the front and back of one structure. Build the telos doc right and the debt taxonomy is its photographic negative, already developed.

**causal chains between primitives — predicted, not anomalous.** 015 treats compound debt as coincident primitives — two debts that happen to co-occur. The cause frame predicts more: the four causes are *not independent*. Final shapes what formal should be. Material constrains which forms are possible. Efficient is shaped by all three. So debt propagates along the same dependencies:
- Spec debt → craft debt. Purpose drifts; the form built for the old purpose is now ill-shaped for the new one. Final-failure induces formal-failure.
- Substrate drift → epistemic debt. The world moves; the because that referenced the old world becomes unrecoverable, because its referent is gone. Material-failure erodes efficient-cause legibility.

These are not coincidences to be itemized — they are the cause-dependencies showing through. The primitives interact causally *because the causes do*. This is the framework's prediction, and it is what 015's coincidence model could not produce.

**what remains open.**
- Multi-axis material. The material cause is composite in software — platform, org (Conway), security landscape, format/dependency ecosystem are all aspects of the material context, and they move independently. The substrate primitive may be one name over a vector. Substrate debt may need to name *which axis of the material cause* moved. Genuinely open: whether substrate is one primitive or a family sharing a cause-slot.
- Recoverability of the causal story. The decomposition tells you *which* primitives are present. It may not tell you the chain — that this craft debt is downstream of that spec debt. List the primitives and the causal arrows may be lost. Whether the chain is always recoverable from a decomposition, or whether it has to be recorded separately at debt-naming time (cf. §3.20 discard-as-act: the because of a structural state is invisible until written), is open. Flag: if the chain is not recoverable post hoc, the decomposition is lossy in exactly the dimension this epistle claims as its advantage.

[→ §1.7, §1.11, §1.12, §3.20, §8.1, §8.2, §8.4, §13.6, Epistle 015]
