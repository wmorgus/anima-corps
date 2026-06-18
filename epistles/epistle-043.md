---
Excavated: 2026-06-18 | Status: semi-liquid
---

Epistle 043 — The Corpus Has No Type
Topic: §42 said corpus docs are dojo surfaces whose canonical form lives in Calliope. But the canonical form has no shape. The corpora say "ratify INTO Calliope" and Calliope's type system has nothing to receive. Define the artifact types that hold corpus material, and the provenance chain that earns them.

The scene that forces this. process.md §3 step 3: "updates the relevant corpus files." logic.md §17.1: "this corpus is itself a frozen artifact." §6a says agent prompts must be Calliope artifacts governed by the §3 cycle. Every one of these names a write INTO Calliope. None says what is written. The corpus is the one body of frozen claims in the whole system that has never been given a Calliope type. §42 closed the directional gap — dojo in, forge out — and then named its own next gap (042 tension 3): which types flow through the dojo. This is that.

The corpus is currently a stack of markdown files in git with §-numbers in them. §39 already ruled that git is authoring/rendering surface, not canonical standing. §42 generalized it. But a canonical claim with no type is a canonical claim that cannot be cited, cannot be superseded through §3.10, cannot be checked for provenance under §3.2. The markdown files have been carrying canonical standing by convention — the exact failure §6a.8 names for builder_philosophy.md (frozen tag on a mutable file), one register up. The corpus is doing to itself what §6a indicts the agent prompts for doing.

---

## (1) The unit is the section, because the unit was always the section

**A corpus_section is one §-addressed section. Not the whole doc; not the individual claim.** The §-addressing system already decided this and has been live for the whole life of the corpus. "→ §3.3" cites the section. A supersession event (§3.10 Aufhebung, an epistle ratifying a change) touches §3.3, not all of logic.md and not claim §3.3.4 in isolation. The citation unit and the supersession unit are the same unit, and it is the section. The type just makes explicit what the addressing already presumed.

Rule out the two wrong granularities, each ruled out by a different existing commitment:

**Claim-per-artifact (§N.M).** logic.md alone holds hundreds of claims. Authoring and ratifying at claim granularity is unauthorable at scale — and worse, it splits a coherent argument cluster into fragments that cannot be reasoned from as a unit. §6.6 (corpus-per-reasoning-surface) wants coherent surfaces, not claim-confetti. Ruled out.

**Whole-doc-per-artifact.** Then you cannot cite §3.3 without dragging all of logic.md. Supersession of one section would re-freeze the whole doc, and §17.4's migration/supersession distinction collapses — every section move would look like a doc-level event. Ruled out.

A section is a coherent argument cluster. That is the right grain for independent Calliope existence: small enough to supersede surgically, large enough to reason from as a whole.

## (2) `corpus_section` — the type

Fields:
- `corpus` — which doc. Extensible project-scoped identifier — not enumerated here; anima's current corpora are illustrative, not normative.
- `section_id` — the §N address: "§3", "§14".
- `section_title` — human-readable.
- `body` — the content.
- `project_id` — corpus is project-scoped. anima's logic.md is anima's; it does not govern calliope.
- `liquidity: frozen` — always. The corpus is frozen reference by definition (§2.3 names the axis; logic.md §17.1 stakes the corpus's position on it). A corpus_section that is not frozen is not corpus.
- `authority.owner_type: human_only` — only humans ratify corpus changes. Agents reason FROM the corpus; only humans ratify the freeze. Agents author the provenance chain (epistle, gravel_record) that earns ratification — the type forbids agent ratification of the freeze, not agent authorship of the record. This is the §6.5 reasoning-obligation boundary made structural: an agent that could ratify a corpus_section could rewrite the coordinates it reasons from. The type forbids it.

**Supersession is the mutation record.** When an epistle ratifies a change to §3, the existing §3 corpus_section is superseded under §3.10 — preserved in history, negated as active, elevated in the successor — and a new corpus_section is created. The supersession trail IS the corpus's change history. No edit-in-place; §6a.8's category error does not get to reappear here. This is the one place the corpus has always claimed supersession-only (§17.1) and never had the substrate to enforce it. The type is the substrate.

Open: §17.4 migration (a claim re-homed between docs, content unchanged) is NOT a §3.10 supersession. Under this type a migration changes `corpus` and keeps `section_id` and `body` — but does it create a new artifact or amend the existing one's `corpus` field? Amending a field is edit-in-place, which the type forbids. Migration-as-supersession-with-identical-body is ugly but type-consistent. Staked toward: migration creates a successor whose body equals the predecessor's, `corpus` changed, marked as §17.4 amendment not §3.10 negation. The successor says exactly what the predecessor said — which is what §17.4 demands. Not fully resolved; the field-level mechanics need a build to settle.

## (3) `corpus_manifest` — the type that makes four-cause coverage checkable

**Project-level index of what corpora exist and what causes they cover. Not a table of contents — it carries the four-cause invariant.** Epistle 028 and §13.6 stake the four-cause hierarchy itself: every account of a built thing covers final (why), formal (the pattern), efficient (how it moves), material (what it's made of). The mapping of those causes onto specific corpus files is not 028's — it lives in the doc headers (process.md's preamble states it outright: "telos.md is the final cause, logic.md the formal cause, substrate.md the material cause; this doc holds the efficient register"). The manifest is where that mapping stops being a fact about anima's five files and becomes a checkable invariant about any project's corpus.

Fields:
- `project_id`.
- `corpora` — list of entries, each naming: corpus name, which Aristotelian cause it covers, the section_ids present, coverage status (frozen / in-progress / absent).
- `four_cause_coverage` — explicit map of final / formal / efficient / material → which corpus addresses each, or marked absent.
- `liquidity: semi_liquid` — the manifest grows as corpora grow; it is the commitment-to-maintain, not a frozen claim. Freezes when a project declares completeness.

**The four-cause structural requirement.** Every project should cover the four causes. Coverage does not mean identical shapes — anima expresses formal cause as logic.md; calliope will express its formal cause differently, maybe under a different name, maybe split across more than one corpus. The manifest does not demand anima's five files. It demands that final, formal, efficient, and material each have a home, and it makes the mapping explicit enough that an absence is visible rather than felt. A project missing efficient-cause coverage is a project that has not said how it moves — an incomplete account of the thing being built.

**Enforcement is staged, not immediate.** Hard four-cause enforcement is a long-term teleological ideal. Calliope does not reject a project for missing a cause on day one — that would make the corpus unwritable, the §2.9 failure of demanding frozen completeness before the work exists. The manifest is the instrument by which coverage is made explicit and tracked toward completeness over time. Calliope enforces the invariant at one specific moment: when a project declares completeness via the corpus_manifest (the semi_liquid → frozen transition). Before that, the manifest records gaps honestly. At that transition, an absent cause blocks the freeze. The invariant is real; it just binds at the declaration, not at every intermediate state. It is Ari's duty as telos authority (Epistle 037) to guide the vibe engineer through the stages of filling any gaps — the manifest is what makes those gaps visible to him.

## (4) The provenance chain — epistle and gravel as types

**The ratification chain must be fully Calliope-native, or every corpus_section is an artifact of unknown provenance.** §3.2 requires recorded + contestable + structurally external. A corpus_section whose because-chain lives only in git markdown satisfies "recorded" by convention and fails it structurally — the record is not in the substrate that makes the claim contestable. The chain epistle → shitcorping → gold-into-corpus currently exists entirely as markdown files in this repo. Two types make it native.

**`epistle`** — the epistle as provenance artifact. process.md already says it: "epistle preserved as provenance artifact" at the frozen transition. Fields: title, number, topic, body, status, excavated_date, project_id. Liquidity tracks the epistle's own lifecycle — the four states in process.md (vapor not stored; liquid / semi-liquid / frozen are). At ratification: frozen. The epistle is the staked argument; its frozen form is the record that this argument is what got considered.

**`gravel_record`** — the shitcorpus record for one epistle. The gravel format in process.md, typed. Fields: source_epistle_id (cites the epistle artifact), gold entries (smelted form + because), gravel entries (dropped + because), tensions (open), smelter_contribution, verdict, and `smith_notes` (optional, free-form). Liquidity: frozen — written once at the end of the shitcorping loop (process.md loop b, step 3), never mutated. The gravel is via-negativa evidence (logic.md §4.9 shitcorpus logic): the shape of what got dropped is part of the record. Frozen because a worked-out sorting is a stake, and §4.9 says a stake that evaporates is not a stake.

`smith_notes` is the smelter's working reasoning during the loop — the panning that found the gold, not the ruling. It attaches to the frozen verdict rather than drifting as a separate liquid artifact. process.md deliberately left loop-internal reasoning untyped as a governed artifact; making smith_notes a field on gravel_record honors that choice while preserving the provenance. The gravel_record is the frozen verdict that earned weight; smith_notes is provenance attached to it, not a coordinate of its own.

**The chain that earns a corpus_section:** corpus_section cites gravel_record cites epistle. Traceable end to end. A corpus_section with no gravel_record in its lineage is an artifact of unknown provenance — §3.2 violated, full stop. This is the structural enforcement of the rule process.md already states (nothing lands in the corpus except through the shitcorping loop). Today that rule is honored by discipline; the citation chain makes it checkable. The lineage is the proof the claim was earned and not asserted.

Open: bootstrap. The hole is structural and present-tense, not just historical. It covers two categories. First, founding sections that predate the epistle/gravel machinery — logic.md §1–§2 were not ratified through a numbered epistle. Second, any in-flight lineage where upstream epistles remain liquid: a corpus_section ratified before 042 and 039 froze has the same defect, an unfrozen upstream in its provenance chain. Either these get retroactive provenance artifacts (honest about being back-filled) or the type permits an exemption with its own marker. An exemption is a §6a.8-shaped hole — "provenance by convention" is exactly what this epistle is closing. Staked toward retroactive back-fill for both categories, marked as reconstruction. Not resolved.

## (5) Same shape, checkable — the corpus is an iceberg too

§42 said every project is an iceberg: human-visible surface, Calliope canonical body. The corpus is the surface that has been faking its own body. Specify the mapping so the self-resonance is checkable, not felt (§7.1):

| Corpus thing | git surface (today) | Calliope canonical (this epistle) | Liquidity | Owner |
|---|---|---|---|---|
| A §-section | markdown in logic.md etc. | corpus_section | frozen | human_only |
| The corpus index | CLAUDE.md structure + reader's head | corpus_manifest | semi_liquid → frozen | human_only |
| An epistle | epistles/epistle-NNN.md | epistle | tracks lifecycle | (provenance) |
| A gravel record | gravel/epistle-NNN.md | gravel_record (carries optional `smith_notes` field — the smelter's panning, attached to the frozen verdict) | frozen | (provenance) |

The inconsistency to look for: any row where the git surface still carries canonical standing after the Calliope type exists. Every "today" cell is a §6a.8 frozen-tag-on-mutable-file hole at the corpus register. The types close them. The dojo direction §42 named (git authoring → §3.10 freeze → Calliope) now has artifacts to freeze INTO. §42 named the door; this epistle builds what passes through it.

## (6) The conviction, not a discovery

This is not "the corpus secretly had types all along and we found them." The honest account: the §-addressing system was built first, as a citation convenience. The conviction that Calliope is the corpus's single home came as conviction (§39), and typing the §-addressing as corpus_section is what makes that conviction enforceable rather than aspirational. The addressing's existence — every "→ §3.3" already treating the section as a unit — is what lets section-per-artifact be stated as the obvious grain rather than argued for from scratch. The type follows the addressing; the addressing embodied a unit-choice nobody had named; the type makes that choice contestable. Same move as §42(7): the name follows the build.

---

## Tensions named, not resolved

**Migration field mechanics (from §2).** §17.4 migration must not be edit-in-place, but it also must not be §3.10 negation — the body is unchanged. A successor-with-identical-body marked as amendment is type-consistent but feels like ceremony. Whether the type needs a distinct migration event class, or rides §3.10 with an amendment flag, is open. The §17.4 distinction is real; its artifact expression is not settled.

**Bootstrap provenance (from §4).** The hole is structural, not just historical. Two categories share it: founding sections that have no real provenance chain (logic.md §1–§2), and any corpus_section whose lineage includes still-liquid upstreams — including anything ratified before 042 and 039 froze. Both produce a weaker §3.2 contestable face than original record. Staked toward back-fill for both, but back-filling a gravel_record after the fact is honest only if marked as reconstruction, not original record.

**Cross-project corpus citation.** corpus is project-scoped (project_id required). But anima's corpus governs calliope's build, and calliope is its own project with its own corpus. Can a calliope corpus_section cite an anima corpus_section as the conviction it inherits? If yes, project-scoping is not isolation, and the manifest's four-cause coverage might be satisfiable by inheritance. If no, every project re-derives its causes from scratch. Not addressed here.

**Does the manifest belong to the corpus or above it?** corpus_manifest is project-scoped and indexes corpora — but it is not itself a corpus_section, and it is semi_liquid where the corpus is frozen. Whether that meta-level wants its own four-cause account is a regress this epistle does not enter. Staked as a question.

[→ §2.3, §2.9, §3.2, §3.10, §4.4, §4.9, §6.1, §6.5, §6.6, §6.8, §6a.8, §7.1, §7.4, §9.3, §13.6, §17.1, §17.4, Epistle 028, Epistle 032, Epistle 037, Epistle 039, Epistle 042]
