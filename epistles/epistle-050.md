---
Excavated: 2026-06-22 | Status: frozen
Shitcorped: 2026-06-22 — verdict liquid, ready to freeze after human step. First pass returned three faults: (1) `corpus_index ∈ REQUIRE_CITES_TYPES` contradicts sibling corpus-type placement in OPTIONAL_CITES and is underargued given `parent_artifact_id` as the load-bearing link; (2) granularity-bet leaked into body as fact on two lines despite being correctly fenced in OPEN; (3) `supersedes / supersedes` duplicate and `§043 gold 3` over-bundling frozen (gold 3 stakes only human_only; frozen is separately warranted). All three fixed: OPTIONAL_CITES family argument added; granularity lines marked predicted-not-measured; supersedes deduplicated; gold 3 / frozen separated with distinct warrants. Second pass: all four focus areas verified verbatim; citations clean. Gold list intact.
---

# Epistle 050 — The Index Is the Form of the Section
Topic: A corpus section needs a retrievable map of its own claims that lives beside it without cutting it apart — the index artifact, derived from the section, encoding its form for retrieval.

---

**The retrieval problem is a granularity mismatch, not a search-quality problem.**

`search_artifacts` now does semantic cosine similarity over full artifact text. That is the right primitive and it works for most types. It does not work for corpus sections, and the reason is structural, not tunable. A `corpus_section` (§043) is 300–2000 words because the citation unit and the supersession unit are the section (§043 gold 2: "→ §3.3" has always cited the section; a §3.10 event has always touched the section). The section is the correct grain to *cite and supersede*. It is the wrong grain to *retrieve against*.

The mismatch produces three failures, and all three are downstream of one cause — the embedding averages a unit that carries many distinct claims:

1. A query about one claim hits the whole section. The score is diluted by every other claim in the body. A section that is the right answer to a narrow question ranks below a section that is loosely about the same topic throughout.
2. The `reasoning` and `alternatives_considered` fields — the *why* — dominate the embedding, and the content body gets truncated. For a corpus section, the body *is* the claim. The Mnemosyne extraction model puts why-what-how on equal footing (the why-what-how chain), but the embedding does not: it over-weights the field that is longest and most discursive.
3. An agent that retrieves the section still cannot navigate to the sub-claim. It pulled 1500 words to use 40 of them. The retrieval succeeded and the agent's context budget paid for the failure.

Tuning the embedding does not fix this. The unit being embedded is heterogeneous by design. You cannot average a heterogeneous unit into a single point and expect the point to answer narrow questions about its parts.

**Chunking is the obvious fix and it is destructive.**

The instinct is to chunk: split the section into claim-sized pieces, embed each, retrieve the piece. This severs the section, and the section is load-bearing in three ways that chunking breaks.

It breaks §-addressing. The §-number addresses the section. Chunk the section and either the chunks share one §-number (and the address no longer resolves to one artifact) or they get sub-addresses the corpus never defined (and every existing citation is now ambiguous about which chunk it meant).

It breaks the supersession unit. §043 gold 2 derived section-granularity from the addressing already in use: claim-per-artifact "splits a coherent argument cluster into confetti that cannot be reasoned from as a unit (§6.6)." A §3.10 supersession is Aufhebung — preserves, negates, elevates — and it operates on the section. Chunk the section and a supersession event has to be reassembled across N chunks, or N supersession events have to be kept consistent. The single atomic mutation becomes a distributed transaction. That is exactly the confetti §043 ruled out, arrived at from the other direction.

It breaks the frozen guarantee. A `corpus_section` is `frozen` and `human_only` (§043 gold 3: an agent that could ratify a corpus_section could rewrite the coordinates it reasons from). Chunking is a transformation of the section's content. Either a human re-ratifies every chunk (the cost of freezing, multiplied by N, on every section) or an agent produces the chunks (and now the frozen, human-only unit has agent-authored derivatives standing in for it at retrieval time — the §6a.8 frozen-tag-on-mutable-content error, one layer down).

Chunking trades a retrieval problem for a citation-integrity problem. That is a bad trade. The citation system is the spine; retrieval is a service on top of it. You do not damage the spine to speed up a service.

**The non-destructive alternative: an index that lives beside the section, not instead of it.**

The corpus already has the shape of the answer. §2.10 (retrieval-target model): a frozen invariant names *where to look*; the fetched content expires at the source, outside the corpus. The frozen thing and the retrieved thing are different artifacts, deliberately. The index artifact applies that split inward. The section stays frozen and whole. The index is a separate, lighter artifact that *points into* the section at claim granularity — a map of the section's claims, retrievable in one search call, that an agent reads first to decide whether to pull the section at all.

The section is the territory. The index is the map. You do not cut up the territory to make a better map; you draw the map at the resolution the traveler needs. This is the same move §2.10 makes for timed facts (point at where to look, do not freeze the fact) turned on the corpus itself: point at the claim, do not chop the section to expose it.

This is what makes the index a **formal-cause artifact**. §13.6 stakes the four-cause hierarchy: final cause is primary, the other three are intelligible only under it, and "final" is a nominal accident of the ordering — the load-bearing claim is the hierarchy, not the list. The index does not carry the section's *final* cause (its telos) or its *material* cause (its full text) or its *efficient* cause (the gravel→epistle chain that ratified it). It carries the section's **form**: the shape of what the section claims, abstracted from the full prose, sufficient to recognize the section by what it argues. The index is the section's form made separately retrievable. It is junior to the section in exactly the way formal cause is junior to final cause — it has direction over nothing on its own; strip the section and the index points at nothing. That juniority is the design constraint, not a weakness: it is why the index can be regenerated, superseded, and even wrong without endangering the section.

**The correct shape: summary plus claims list. The other two candidates are either redundant or unstable.**

Three shapes were proposed. Argue them from what retrieval actually needs, not from what sounds useful.

The need is precise: an agent issues one semantic query and must get back enough to decide *which section* answers it and *which claim within that section* does the answering — without reading the section. The shape must (a) be retrievable in a single `search_artifacts` call, (b) embed well under cosine similarity, (c) point at claim granularity, and (d) survive the section being superseded.

*Summary plus claims list* — a 2–3 sentence thesis summary, then each claim the section makes as one line — meets all four. The summary gives the embedding a coherent thesis-shaped vector instead of an averaged body. The claims list is designed to give claim-granularity retrieval *without chunking the source*: each claim line is short enough that its embedding should be sharper than a whole-section average (this is the load-bearing empirical bet, fenced in [OPEN]). When an agent's query matches a claim line, the agent learns the §-number and the specific claim, then decides whether to pull. This is the §043 grain insight inverted: §043 said do not make each claim an artifact (confetti). The index makes each claim a *line in one artifact* — claim-level retrieval, section-level citation, no severing.

*Tag cloud* — canonical terms and §-numbers the section uses, cites, or is cited by — is the wrong primitive for this layer, and it is redundant. It is a structural/relational index, and Calliope already holds the relational structure as typed edges (`elaborates`, `depends_on`, `supersedes`, and the §043 citation chain). A tag cloud re-encodes, in lossy free text, what graph traversal already answers precisely. It does not retrieve at claim granularity — a term is not a claim — and it embeds poorly: a bag of terms has no thesis-shaped vector. The relational layer is real and worth having; it is not the index, and it should not be rebuilt inside one. Build it as edges, traverse it as edges.

*Q&A pairs* — anticipated questions, each answered by a pointer to the section and claim — is the most seductive and the least stable. It retrieves well (the question is exactly the query shape an agent will issue). But it requires the index author to enumerate the questions an agent might ask, and that set is unbounded and changes as the agents and their tasks change. A claims list is closed by the section: the claims are *in* the section, finite, and stable as long as the section is frozen. A Q&A set is open against the world of possible queries: it goes stale not when the section changes but when the *questions* change, which the section's frozen status cannot guarantee. An index that decays independently of its source violates the regeneration contract below — you could not know it was stale by looking at the section. Q&A pairs answer "what might someone ask," which is unstable; the claims list answers "what does this section claim," which is fixed by the frozen section. Fix what is fixable.

So: summary plus claims list. Not a combination — a combination would re-import the tag cloud's redundancy and the Q&A set's instability. One shape, chosen because it is the only one closed by the section it indexes.

[DRAFT NOTE: the claim that "each claim line embeds sharply enough for claim-granularity retrieval" is a prediction about embedding behavior, not a measured result. It is the load-bearing empirical bet of this epistle. It should be staked as a `conviction_stake` (§4.9) with `null_result_behavior: update_priors`, and tested by an `empirical_record` measuring retrieval precision of claim-line queries against the index versus full-text queries against the section. If claim-line embeddings do not separate better than full-section embeddings, the shape argument holds but the granularity payoff does not — and the fallback is summary-only, which still fixes failures 1 and 2 but not 3. Do not freeze the granularity claim until the empirical_record exists.]

**The Calliope type: `corpus_index`, derived, semi_liquid, pinned to a section version.**

The index is not a `corpus_section`. It carries no canonical standing, makes no claim of its own, and is not human-ratified. It is *derived from* a corpus_section. Proposed type name: `corpus_index`.

Envelope (mapping to the live `ArtifactCreate` schema):

- `type: corpus_index`
- `liquidity: semi_liquid` — regenerable from the source, but pinned to a version of it. Not `liquid` (it is not freely rewritable scratch) and not `frozen` (it must regenerate when the section is superseded). `semi_liquid` is the exact register: stable until its source moves, then regenerated. This matches `context_snapshot` and `backlog_item`, which are semi_liquid for the same reason — derived, stable, regenerable on a triggering event.
- `parent_artifact_id: <corpus_section id>` — the index's source. This is the load-bearing link. The schema's `parent_artifact_id` is the right field (it must not be silently dropped, per the CAL-04 envelope contract); `source_artifact_id` is not in the schema and should not be invented when `parent_artifact_id` carries exactly this meaning.
- `authority.owner_type: any_agent` — Mnemosyne writes it; no human ratification gate. The section is human_only and frozen; the index is neither. These are distinct properties. §043 gold 3 stakes human_only: agents cannot *ratify the coordinates* — the index ratifies nothing, it describes. The frozen status of the section is set by the ratification step (§043 §2 + schema); the index does not inherit it because it is derived, not ratified. An agent producing a description of a frozen section does not touch the freeze.
- `cites: [<corpus_section id>]` — every other corpus-provenance type (`corpus_section`, `corpus_manifest`, `epistle`, `gravel_record`) sits in `OPTIONAL_CITES_ARTIFACT_TYPES` by deliberate decision. The index follows that family: the cite is conventional, not schema-enforced. The structural guarantee that every index has a section behind it is already carried by `parent_artifact_id` — the load-bearing link. Forcing `cites` into `REQUIRE_CITES_TYPES` would duplicate enforcement already present and inconsistent with the corpus-provenance family convention.
- `supersedes` edge — set when regenerating against a superseded section (below).

Content schema (`CorpusIndexContent`):

- `section_id: str` — the §-address of the indexed section (e.g. "3.15"), so an agent can resolve the pointer without a second lookup.
- `corpus: str` — the source corpus identifier. Extensible project-scoped string, not an enum — §043 gravel 2 dropped the hard-coded corpus enum as the §6a.8 error miniaturized. Do not reintroduce it here.
- `summary: str` — 2–3 sentences. The section's thesis, embedded as a thesis, not an average.
- `claims: list[str]` — one line per claim. Closed by the section.
- `source_version: int` — the `version` of the parent corpus_section this index was generated against. The pin. An index whose `source_version` is behind its parent's current version is stale by definition, and detectably so — no convention required, just a version comparison.

The whole-artifact embedding is now summary-plus-claims rather than full body — short, claim-dense, thesis-shaped. That is the structural design: the thing that gets embedded is built to be embedded. Whether the resulting embeddings separate at claim granularity is the empirical question this design is meant to test, not a fact it establishes.

**The production process: Mnemosyne produces it from the frozen section, regenerates it on supersession.**

Humans do not write indexes. The corpus_section is the human-ratified artifact; the index is downstream of the freeze and mechanical relative to it. The producer is Mnemosyne — the extraction agent — applying the why-what-how extraction model to a single frozen section: the summary is the *what* compressed; the claims list is the *what* enumerated. This is the extraction model pointed at the corpus instead of at code.

The trigger is the freeze. When a corpus_section is ratified to `frozen`, Mnemosyne generates its `corpus_index`. The index's `source_version` records the version it indexed.

Regeneration on supersession is the non-negotiable half. When a section is superseded via §3.10, its index is now indexing a negated claim. The index must be regenerated against the successor, and the old index superseded in lockstep — a `supersedes` edge from the new index to the old, mirroring the section's own supersession. This is what makes the index safe: it has no independent lifecycle. It moves when and only when its section moves, and the `source_version` pin makes a lagging index detectable rather than silently wrong. An index that could go stale on its own — Q&A pairs decaying as questions change — would not have this property, which is the second reason that shape was dropped.

The discipline in one line: the index is regenerated, never edited. Same as the section it serves, same as §3.10 itself — preserve, negate, elevate, never edit-in-place.

**Index artifacts are the precondition for chunking, not a substitute argument against it.**

This epistle rejects chunking *the source*. It does not reject claim-granular retrieval — it delivers it, non-destructively. And it makes intelligent chunking *possible later*, if chunking is ever warranted, by supplying the thing chunking actually requires: a claim-level map of where the seams are.

Naive chunking splits on token windows or paragraph breaks — boundaries that fall mid-claim and produce the confetti §043 ruled out. The reason naive chunking is destructive is that it chunks *before* knowing what the claims are. The claims list is precisely that knowledge. If a future build wants to chunk for some purpose this epistle does not foresee, it should chunk *at claim boundaries the index already identified* — and even then, the chunks would be derived retrieval artifacts pointing into the frozen section, never replacements for it. The order is fixed: know the claims, then decide whether to chunk. The index is step one. Chunking, if it ever comes, is a possible step two that the index makes safe rather than reckless. They are not the same thing and not competitors; the index is the precondition.

**One Home holds: the index lives in Calliope, not in git.**

Epistle 039 (One Home): the corpus's canonical artifacts live in Calliope. The index is a Calliope artifact — `parent_artifact_id` to the section, retrievable by `search_artifacts`, superseded by edge. It does not live as a sidecar file in the corpus repo. A git-side index would be a frozen-tag-on-mutable-file error (§6a.8) and could not participate in supersession or retrieval. The section's home is Calliope; the index lives in the same home, one register below the section, as the section's retrievable form.

**[OPEN]**

- **Sub-corpus indexing for very large sections.** A 2000-word section may carry 15+ claims. Does the claims list itself eventually need its own retrieval grain, or is a 15-line list always retrievable as a unit? Suspected fine as-is (the list is short relative to the body), but the threshold where a claims list becomes its own granularity problem is unmeasured. This is the §043 grain question re-asked one level down, and it may have the same answer (the section is the unit) or a different one.
- **Cross-corpus claim collision.** Two sections in two corpora may state near-identical claims (§15.12: cross-corpus epistemic epidemiology). Claim-level retrieval makes such collisions *visible* for the first time — two index claim-lines surfacing on one query. Is that a feature (the index surfaces a real §15.12 tension that whole-section retrieval hid) or noise (the agent now sees two answers and cannot rank them)? Genuinely unresolved; depends on whether surfaced collisions are actionable.
- **The granularity bet (carried from the DRAFT NOTE).** Whether claim-line embeddings separate measurably better than full-section embeddings is the empirical question this epistle rests its granularity payoff on. The shape argument (closed-by-section, single-call, version-pinned) holds regardless. The claim-granularity benefit does not, until measured. Stake and test before freezing that half.
- **Manifest-level indexing.** §043's `corpus_manifest` is itself an artifact one meta-level up. Does the manifest get a `corpus_index`, or is the manifest already index-shaped enough that indexing it is the manifest-regress §043 tension 4 named? Not entered here.

[→ §1.12 — registers and the intent spine; the index operates one register below the section, as the section's form. §2.10 — retrieval-target model; the frozen-invariant / expiring-content split applied inward. §3.3 — the external validator; the index describes, it does not ratify. §3.10 — supersession as Aufhebung; the index regenerates in lockstep, never edits. §6.6 — corpus-per-reasoning-surface; the index serves retrieval against that surface without becoming one. §6a.8 — frozen-tag-on-mutable-content; why the index lives in Calliope and is never edited in place. §13.6 / §13.6a — four-cause hierarchy; the index is the section's formal cause, junior to the section's final cause, with direction over nothing on its own. §15.12 — cross-corpus epistemic epidemiology; claim-level retrieval as a new collision surface. Epistle 039 — One Home; the index lives in Calliope, not git. Epistle 043 — corpus_section as the citation-and-supersession unit; the index is derived from it and inverts its grain insight, claim-per-line instead of claim-per-artifact.]
