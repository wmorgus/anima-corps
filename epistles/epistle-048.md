---
Excavated: 2026-06-22 | Status: liquid
Shitcorped: 2026-06-22 — verdict liquid, ready to freeze after the human step (gravel/epistle-048.md). All six claims earn weight. Earned: the telos-is-a-coverage-claim derivation (claim 1 — telos.md "floor it stands on"/"those artifacts live here" + §3.3 single-source-of-truth + §1.12 self-named as the territory's taxonomy; "floor not a shelf" earned); the coverage inventory verified structurally against types.py (claim 2 — intent-spine/deliberation/anima-native present and modelled; contract/operational/verification absent; `build_verification` is pipeline-internal, not a §1.12 verification register); the execution_prompt inversion keystone (claim 4 — §1.12 names prompt-as-artifact first-class verbatim, execution_prompt deprecated in types.py with the exact pipeline-chain reason quoted, no successor type, §15.2 confirmed [OPEN]; the deprecation reason self-incriminates by naming chain-membership as the criterion for belonging); the telos-derived (not dogfood-derived) generalization (claim 5 — project-independence is structural via ruling-out #6); the derived MVP ordering contract→operational→verification (claim 6 — contracts are the objects of §3.3 contestation; operational on §8.4 substrate debt with verbatim §1.12 failure modes; verification logically downstream since attestation presupposes the commitment). Soft spots (none touching a warrant, none changing a verdict): the "near-entirely absent" inventory ignores two partial/adjacent types (`data_provenance_contract`, schemaless `deployment_record`) that prove the point rather than refute it; claim 3's "coverage layer vs validation layer" failure-location is a two-hop derivation (through the telos's single-source-of-truth) stated as a one-hop reading of §3.3; execution_prompt and §1.12's prompt-as-artifact are treated as plainly one register when they may be cousins (coverage conclusion holds either way); the verification-second-order step is compressed. Both Opens (design-criterion-not-type-list; MVP scoping; execution_prompt supersession) real and correctly left open. Tension flagged for freeze: governed-addition (value-ordering #4) vs. derive-downward criterion — reconciles at the first Open, worth naming explicitly. Status advanced to semi_liquid pending the human freeze step.
Shitcorped: 2026-06-22 (re-pass after two surgical edits) — verdict liquid, clean to freeze. Both edits adopt fixes the prior gravel recommended and neither introduces a new gap. New inventory sentence (`data_provenance_contract` field-level provenance not a §1.12 data-schema register; `deployment_record` enum-present but schemaless — no `_CONTENT_SCHEMAS` entry) re-verified exact against types.py and closes soft-spot #1; "their presence proves the point" earns its close via the same-line criterion (name-presence ≠ register-holding). New Open sentence faithful to telos value-ordering #4 (verbatim "governed addition, not expedient escape hatches"), names the derive-downward/governed-addition seam the prior pass flagged for freeze, and correctly poses it as live implementation work rather than claiming resolution — the residual need-triggered vs. taxonomy-triggered seam is left for the implementation pass, which is honest for an Open. No new logical gap or contradiction with §1.12/§3.3.
---

Epistle 048 — The Map and the Pipeline
Topic: Epistle 039 staked Calliope as single source of truth; this epistle stakes what that claim requires of the type system — Calliope must be able to hold the full §1.12 register space, not only the artifact types the build pipeline produces.

---

**Calliope's telos is a coverage claim.**

Calliope's telos says it is "the floor the Anima system stands on" and that "every artifact in the Anima system answers 'does this serve the telos?' — those artifacts live here." That is not a statement about what the build pipeline produces. It is a statement about the complete territory of any software system Anima is asked to govern. §1.12 is the taxonomy of that territory: seven register groups, from intent spine through anima-native, that together constitute software-as-language. If Calliope cannot hold what §1.12 names, it cannot be the floor — it is a shelf.

The derivation is direct. §3.3 requires that the externality primitive — the thing external validation goes through — be a single source of truth for the governed system. Single source of truth is a coverage claim. A store that can hold five of the seven register groups is not a single source of truth; it is a complete record of the five it covers and silent on the other two. Agents contesting from that store contest from an incomplete map.

**The current taxonomy maps the pipeline, not the system.**

The current ArtifactType enum covers the intent spine (user_story, test_spec, sprint_contract), the deliberation registers (architectural_decision, design_proposal), and the anima-native registers (agent_capability_map, routing_decision, agent_constellation) well. The transition registers are partial: pull_request is present; migration scripts, post-mortems, and incident records are absent. The remaining three groups — contract registers, operational registers, and verification registers — are near-entirely absent. Two types gesture toward this space: `data_provenance_contract` is a provenance contract for longitudinal study data fields, not a general §1.12 data-schema register; `deployment_record` is in the enum but carries no typed content model. Their presence proves the point — a partial type that does not hold the register is not coverage.

What is missing: API contracts, data schemas, event schemas, permission schemas, SLAs. Runbooks, deployment manifests, dependency manifests, configuration, feature flags, monitoring config. Security audits, compliance certifications, performance benchmarks.

This is not a random omission. The types that exist are the artifacts the build pipeline produces — the work of building software. The types that are missing are the artifacts that describe what a software system IS — what it commits to, what it runs on, what validates that its commitments hold. The taxonomy reflects pipeline concerns rather than §1.12's register space. The result is a store that knows a great deal about how Anima builds and almost nothing about what it builds.

**The pipeline and the system are not the same thing.**

The pipeline is what Anima does: the build loop, the ratification cycle, the sprint contract to pull request chain. The system is what the software being built is — the contracts it makes with callers, the environment it requires to run, the attestations that its commitments hold. A complete map holds both. Calliope currently holds mostly the first.

The failure this produces is not a validation failure — the artifacts Calliope does hold are correctly typed and validated. It is a coverage failure. An agent reasoning from Calliope about a system Anima governs can retrieve what was built but not what exists. It cannot answer: what does this system promise callers? What does it depend on to run? Has the threat model been evaluated? Those answers are not in the store. The §3.3 externality requirement fails not at the validation layer but at the coverage layer — the questions an external party would need to ask to contest are answerable nowhere in Calliope.

**The execution_prompt deprecation is the coverage failure made concrete.**

§1.12 names prompt-as-artifact as a first-class anima-native register: "the because for agent behavior, treated as a first-class ratifiable artifact." Its failure mode: "prompt governance gap (→ §15.2) — behavior ungoverned when prompt lives outside ratification." The register exists because AI-augmented systems need a governed home for the artifacts that determine agent behavior.

execution_prompt was deprecated with this reason: "Direct execution removed it from the active audit chain. Active chain: sprint_contract → build_decision → pull_request → build_verification."

The deprecation is correct that execution_prompt fell out of the pipeline audit chain. It is incorrect in treating that as the closing argument. The pipeline audit chain is a pipeline decision. §1.12 is the authority on what registers are first-class. The deprecation inverted that relationship — it treated the pipeline as the standard and the corpus taxonomy as advisory, and removed a §1.12 first-class register because the pipeline no longer needed it.

No successor type was added. The §1.12 register is now unserved: execution_prompt deprecated, no replacement, §15.2's prompt governance gap still open. The pipeline ate the system register it was supposed to be governed by.

The inversion is the pattern to name. Once the pipeline becomes the criterion for what belongs in the type system, every register the pipeline does not actively produce becomes a candidate for removal or non-addition. The map shrinks to the pipeline, and the pipeline calls itself complete.

**The argument does not belong to the dogfood case.**

Calliope and aZero are the current build targets — the first project through the door. The gap is visible here because we are using Anima to build Anima and can feel what is absent. But the argument is not about this build.

Any project that hands itself to Anima — a team governing an API layer, a data pipeline, a production service — hits the same wall. Where does the OpenAPI spec live? The deployment manifest? The SLA? The answer is supposed to be Calliope. Right now it is nowhere. The type system does not support it. The project can bring its user stories, acceptance criteria, and pull requests, and Calliope will hold them well. It cannot bring what the system IS, because the type system has no slots for it.

Calliope's telos says it is the externality primitive for any Anima-conformant system. That claim is binding regardless of which system is at hand. The current type system fails it regardless of which system is at hand.

**What follows: the minimum viable extension.**

The full §1.12 register space is the goal; it is not the immediate work. The minimum viable extension is derived from §3.3's contestability floor — which missing registers make external contestation impossible?

Contract registers first. Without API contracts, data schemas, event schemas, permission schemas, and SLAs in Calliope, the system's commitments to the outside world have no home in the store. An external party cannot contest against a commitment that is not there. This is §3.3's requirement stated as a deficiency: the externality check cannot run on a commitment that lives outside the externality primitive.

Operational registers second. §1.12 names the failure mode: "environment becomes silent author of intent." A deployment manifest not in Calliope means the running system can drift from what the store says exists — the substrate debt pattern §8.4 names. Configuration not in Calliope means the environment governs behavior without a ratification record. These are not edge cases; they are the normal operating conditions of any production system. Migration scripts belong here: every schema transition has a because, and without it in Calliope, substrate debt accretes with no trail.

Verification registers are second-order. A security audit attests that a commitment holds; the attestation presupposes the commitment. Add contract registers first; the attestation layer follows.

The MVP is not all of §1.12. It is the registers load-bearing for the externality claim — the ones whose absence makes §3.3 fail at the coverage layer before it even reaches the validation layer.

**Open.**

- *The design criterion, not the type list.* The actionable conclusion of this epistle is not "add these types." It is that the design criterion for Calliope's type system must be §1.12's full register space — derived downward from the taxonomy, not grown upward from the pipeline's artifact needs. Without that criterion staked, the taxonomy will continue to grow ad hoc from inside the pipeline, and the coverage failure will recur. One seam to name at implementation: telos value-ordering #4 requires that new types enter through governed addition — the derive-downward criterion sets the target set; governed addition is how the target set is reached. These are compatible, but the seam between them is where the expansion work lives.

- *Scoping the MVP additions.* Which specific types constitute the minimum viable contract and operational registers is unstaked here. The minimum viable extension argument establishes the ordering and the criterion; the specific additions require a separate pass against §1.12's register rows.

- *execution_prompt supersession.* The deprecation should be a supersession: a type deprecated without a successor leaves the register unserved. What the successor type should look like — a general prompt-as-artifact type, or something more specific to agent behavior specification — is open. The absence of a successor is a gap the MVP pass should address.

[→ §1.12, §3.3, §3.3a, §4, §5.2, §8.4, §15.2, Epistle 039, telos.md (Calliope)]
