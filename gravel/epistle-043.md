---
Source: epistles/epistle-043.md
Shitcorped: 2026-06-18
---

# Epistle 043 — The Corpus Has No Type // Gravel Record

## Gold (earned weight)

1. **A canonical claim with no Calliope type cannot be cited, superseded via §3.10, or checked for provenance under §3.2.** *Because:* derives the type-gap failure from three frozen claims at once. Rules out "markdown with §-numbers is good enough" by showing it fails the structural requirements, not merely the convenient ones — citation, supersession, and provenance all need a unit Calliope can hold, and a markdown heading is not one. The corpus has been carrying canonical standing by convention: the §6a.8 frozen-tag-on-mutable-file error one register up.

2. **The citation unit and the supersession unit are the same unit, and it is the section.** *Because:* derives section-granularity from the §-addressing system already in use, not from preference — "→ §3.3" has always cited the section, and a §3.10 event has always touched the section. Rules out the two wrong grains, each by a different existing commitment: claim-per-artifact splits a coherent argument cluster into confetti that cannot be reasoned from as a unit (§6.6), and whole-doc-per-artifact collapses §17.4's migration/supersession distinction by making every section move a doc-level event. The type makes explicit what the addressing always presumed.

3. **`corpus_section` must be `human_only` because an agent that could ratify a corpus_section could rewrite the coordinates it reasons from.** *Because:* converts the behavioral rule (agents reason FROM the corpus, not TO it) into a structural type constraint, derived from the §6.5 / §3.3 collapse it prevents. Rules out agent ratification of corpus changes — not agent authorship of the provenance chain that earns ratification. The type forbids the act of freezing, not the contribution to the record that makes a freeze legible.

4. **`corpus_manifest` converts the four-cause structural requirement from a fact about anima's files into a checkable invariant about any project's corpus, enforced at the completeness declaration.** *Because:* stakes the four-cause requirement (Epistle 028, §13.6) as a general property rather than an anima-specific accident, and binds enforcement at the semi_liquid → frozen transition. That binding respects §2.9 — it does not demand frozen completeness before the work exists — while still making the invariant real. Rules out "we'll get to the missing cause eventually" as a silent status quo: the manifest makes the gap visible and blocks the freeze if a cause is absent.

5. **The provenance chain corpus_section → gravel_record → epistle is the structural enforcement of "nothing lands in the corpus except through the shitcorping loop."** *Because:* converts a discipline into a lineage check. A corpus_section with no gravel_record in its lineage is a §3.2 violation — recorded by convention, not by substrate. Rules out back-door corpus additions. The citation chain is the proof the claim was earned and not asserted.

6. **The epistle, gravel_record, and smith_notes (as a field on gravel_record) are Calliope-native artifact types; the provenance chain must be native or §3.2's contestable face is convention, not substrate.** *Because:* stakes that the ratification chain cannot live only in git markdown and still satisfy §3.2's "structurally external" requirement. process.md already says "epistle preserved as provenance artifact" — this types that claim. The gravel_record is the frozen verdict; smith_notes as an optional field on it is the smelter's working reasoning attached to the frozen ruling, honoring process.md's deliberate choice not to govern loop-internal reasoning as a separate artifact.

## Gravel (dropped)

1. **`smith_notes` as a standalone artifact type.** Reaching toward: typing the smelter's loop-internal reasoning so the panning that found the gold is preserved. *Because:* process.md deliberately left loop-internal reasoning untyped as a governed artifact — its "iterative not linear" section is silent on the governance of reasoning shape, and that silence is a choice. Typing smith_notes separately would govern what process.md chose to leave ungoverned. Demoted to an optional field on gravel_record: attached to the frozen verdict it earned, rather than drifting as its own liquid artifact. The provenance is kept; the standalone type is dropped.

2. **A hard-coded `corpus` enum ("logic / rhetoric / process / substrate / telos").** Reaching toward: a closed, validatable set of corpus names on the `corpus` field. *Because:* the list is already stale against §1.16 (composition.md) and glossary.md, and a frozen enum inside a type definition is the §6a.8 error this epistle indicts, miniaturized — a fixed claim baked into mutable-by-design surface. Dropped; the field is an extensible project-scoped identifier. anima's current corpora are illustrative, not normative.

3. **"Agents never write TO the corpus."** Reaching toward: the human_only ratification constraint (gold 3). *Because:* the formulation is too broad — §4's provenance chain (epistle, gravel_record) is explicitly agent-authored. Corrected to distinguish ratification (human_only) from authorship of the chain (agent work that earns the ratification). The blanket prohibition was in tension with the type's own provenance mechanism.

4. **§6.4 / §4.4 miscitations.** Mechanical. Fixed in the epistle body, no argument carried.

## Tensions (open)

1. **Migration field mechanics.** §17.4 migration (a claim re-homed between docs, body unchanged) is not a §3.10 supersession (body negated and elevated), but the field-level encoding is open. Amending a `corpus` field is edit-in-place, which the type forbids; a successor-with-identical-body marked as a §17.4 amendment is type-consistent but feels like ceremony. Staked toward migration-as-successor-with-identical-body marked as a §17.4 amendment, not a §3.10 negation. Whether the type needs a distinct migration event class or rides §3.10 with an amendment flag needs a build to settle.

2. **Bootstrap provenance.** The hole is structural and present-tense, not only historical. It covers two categories: founding sections that predate the epistle/gravel machinery (logic.md §1–§2), and any in-flight lineage where upstream epistles remain liquid — a corpus_section ratified before 042 and 039 froze has an unfrozen upstream in its provenance chain, the same defect. Either category produces a weaker §3.2 contestable face than original record. Staked toward retroactive back-fill for both, marked as reconstruction, not original record. An exemption marker would be a §6a.8-shaped hole — provenance by convention — which is exactly what this epistle closes. Not resolved.

3. **Cross-project corpus citation.** `corpus` is project-scoped, but anima's corpus governs calliope's build. Can a calliope corpus_section cite an anima corpus_section as the conviction it inherits? If yes, project-scoping is not isolation, and the manifest's four-cause coverage may be satisfiable by inheritance rather than re-derivation. If no, every project re-derives its causes from scratch. Not addressed here.

4. **Manifest meta-level regress.** corpus_manifest is project-scoped, semi_liquid, and not itself a corpus_section. Whether that meta-level wants its own four-cause account is a regress this epistle does not enter. Staked as a question.

## Smelter's contribution

- Caught that the epistle indicts frozen-tag-on-mutable-content while planting two small instances of the same error: the hard-coded `corpus` enum, and a bootstrap scope drawn too narrowly. Both corrected — the enum dropped to an extensible identifier (gravel 2), the bootstrap tension widened (below).
- Sharpened "agents never write" to distinguish ratification from authorship. §4's agent-authored provenance chain was in direct tension with §2's blanket prohibition; the type forbids the freeze, not the record (gold 3, gravel 3).
- Pressed smith_notes against process.md's deliberate non-typing choice and landed it as an optional field on gravel_record rather than a separate type — honoring the choice without losing the provenance (gold 6, gravel 1).
- Widened the bootstrap tension from historical (founding sections) to structural-present: any in-flight unfrozen lineage carries the same §3.2 defect, including corpus_sections ratified before 042 and 039 froze (tension 2).

## Verdict

Status: semi-liquid (shitcorped, not yet ratified into corpus)

043 types the corpus's canonical form for the first time — corpus_section, corpus_manifest, epistle, gravel_record — converting the §3.2 structural requirement from convention to substrate and deriving the human_only ratification constraint from the collapse it prevents. Four tensions stay open: migration field mechanics, bootstrap provenance, cross-project citation, and the manifest meta-level regress. The migration and bootstrap tensions each need a build to settle; cross-project citation and the meta-level regress are staked as questions, not directions. Awaits ratification into the corpus.
