---
Excavated: 2026-06-08 | Status: liquid
---

Epistle 033 — Corpus Hygiene Pass: 2026-06-08
Topic: Nine mechanical defects in the corpus as of today, one missing §-claim that leaves §6.6 citing a phantom address, and four epistles whose gold never ratified — named and deferred.

---

**Premise.** A corpus accumulates drift the way code does: broken citations, stale cross-references, claims that landed structurally but whose warrants were never staked as §-numbers. The cost is the same — downstream readers reason from a surface that implies more solidity than the provenance chain actually holds. This epistle names every such gap visible on 2026-06-08 and stakes one missing claim that other §-numbers already depend on.

---

## Mechanical fixes (A1–A9)

**A1. `glossary.md` → `corpus_vocab.md` in logic.md.** §1.12 and §1.16 both read `glossary.md`. The file on disk is `corpus_vocab.md`; telos.md already uses the correct name. Two stale references. Fix: update both §-citations to `corpus_vocab.md`.

**A2. Phantom §20 citations in corpus_vocab.md.** The "shitcorp" entry cites §20.3 and §20.4 as provenance. §20 does not exist in logic.md. Source: epistle-013's gold was never ratified into the corpus — those §-numbers are anticipatory, not real. Current citation is broken provenance. Replace with `[§3.20, §6.6, epistle-013 (pending ratification)]` — the actual §-claims that ground the concept plus honest flagging that the epistle-013 ratification is incomplete. The phantom citations are the symptom; the root is A2's companion flag in section C below.

**A3. Broken markdown hyperlinks in rhetoric.md.** Preamble and §4.2 carry `[corpus_logic.md](corpus_logic.md)` — standard markdown hyperlinks that resolve to nothing on disk (the file is not at that path relative to rhetoric.md's location). The `[→ corpus_logic §X]` citation notation is intentional: Calliope artifact IDs, not filesystem paths, and it stays. The broken hyperlinks are a different form: they are attempting to be clickable filesystem links and failing. Fix: remove the markdown hyperlink wrapping; leave the prose reference intact as plain text. Citation notation unaffected.

**A4. §15.17/§15.18 inversion in logic.md.** §15.18 appears at line 612; §15.17 at line 614. Ascending §-order is violated. Swap to restore: §15.17 (reading-skill residual) before §15.18 (Hermes self-application problem at intake). Content unchanged; order restored.

**A5. Wrong Source header in gravel/epistle-016.md.** Line 2 reads `Source: epistles/epistle-013.md`. Should be `epistle-016.md`. A transcription error; the gravel record's identity is wrong.

**A6. process.md conflates gravel file with shitcorpus.** Line 47 reads: "The gravel file is the shitcorpus: permanent record of what was kept, what was dropped, and why." The gravel file is a record *in* the shitcorpus — one contribution to the aggregate (§6.6). The shitcorpus is the aggregate of all discard records. The sentence as written conflates part and whole. Fix: "The gravel file is a record in the shitcorpus — permanent record of what was kept, what was dropped, and why for one epistle. Future prospectors do not re-pan the same gravel."

**A7. Shitcorpus-as-aggregate clarification.** Companion to A6, tighter. process.md should carry one explicit sentence: "The gravel file is a record in the shitcorpus, not the shitcorpus itself." The shitcorpus is the aggregate (§6.6/corpus_vocab.md "gravel/shitcorpus" entry); a per-epistle gravel file is one contribution to it. Currently nowhere stated in process.md; readers can silently equate the two.

**A8. telos.md overclaim on ur-software.** Derivation bridge line reads: "distinct telos docs of their own." No ur-software telos docs exist. The five ur-software files are frozen reasoning-surface coordinates — the what of each surface's world of forms, not the why. Telos docs for each surface would be warranted; they have not been written. Correct to: "Pavel's reasoning surface (§6.6); frozen coordinates for positional diagnosis. Telos docs for each surface are warranted but do not yet exist."

**A9. CLAUDE.md VERSION section duplicates process.md.** CLAUDE.md's "Versioning — git mechanics" section carries semver semantics (what patch/minor/major mean for the corpus). Those semantics now live in process.md (the process authority; Epistle 032). CLAUDE.md carrying a second copy means two authoritative sources for the same claim — precisely what §17.1 rules out. CLAUDE.md should hold only the git mechanics: the `git tag` command, the `VERSION` update step, the anima-core `CORPS_VERSION` fidelity pin. Semver semantics: pointer to process.md only.

---

## Missing §-claim (B1)

**B1. Stake `reasons_against` vs. `reasons_from` as §3.21.**

§6.6's shitcorpus entry reads: "The relationship between filtering agents and this corpus is `reasons_against`, not `reasons_from` (§6.3a)." §6.3a does not exist in logic.md. The distinction is cited from a phantom address.

The distinction is load-bearing — not decorative. Two claims hang on it:

*First.* The shitcorpus is evidence, not waste. A filtering agent that reads it *reasons against* it — uses the gravel record to avoid re-traversing discarded reasoning. This is structurally different from reasoning *from* a corpus as frozen coordinates (§2.5). A corpus you reason-from is ground; a corpus you reason-against is via negativa. Same artifact class, different epistemic relationship.

*Second.* The distinction explains why the shitcorpus cannot be collapsed into the logic corpus. §6.6 commits both corpora; they are different corpora because the agents relate to them differently — not because the content is organized differently. One is frozen coordinates you stand on; one is the shadow-shape of what was discarded, which you navigate around.

§3 is the right home: ratification and governance is where discard-as-act already lives (§3.20), and the `reasons_against` relationship is the governance complement — it names what the shitcorpus is *for* in the agent's reasoning posture, as opposed to what it records. Proposed address: **§3.21** (next available after §3.20).

The §-claim to stake:

> §3.21 **`reasons_against` vs. `reasons_from`.** A corpus an agent reasons *from* functions as frozen coordinates — §2.5 ground. A corpus an agent reasons *against* functions as via-negativa navigation: the agent reads the gravel record to avoid re-traversing discarded reasoning, not to stand on it. The two relationships are structurally distinct even when the artifact class is the same (frozen corpus entry). The shitcorpus (`corpus_shitcorpus`, §6.6) is the committed instance of the `reasons_against` relationship: filtering agents consult it to avoid re-discovering what was already discarded with a because. Rules out: collapsing the two relationships by artifact class; treating the shitcorpus as a reasoning surface equivalent to corpus_logic; reading `reasons_against` as a weaker or provisional version of `reasons_from`.

On ratification, update §6.6's shitcorpus paragraph: replace `(§6.3a)` with `(§3.21)`.

---

## Flags for separate ratification (C1–C4)

Four epistles landed structurally — their artifacts exist — but the warrants behind those artifacts were never staked as §-claims. Not ratified here. Named so the phantom citations they produce are visible and queued.

**C1. Epistle-013 (The Word Earns Its Place Twice) — four unratified gold claims.** Two-warrant separability; read-time vocabulary compression; accidental/essential cut; immune-function telos of shitcorp. The "shitcorp" entry in corpus_vocab.md is currently backed by phantom §20.3/§20.4 citations (see A2 above). Until epistle-013's gold ratifies, those four claims have operational presence — the corpus behaves as though they are staked — but no §-address. Deferred because the ratification is a full shitcorping pass, not a housekeeping fix. Fix A2 closes the broken-citation surface; the underlying gap remains.

**C2. Epistle-014 (The Vocabulary Corpus) — G4 and G5 never staked.** corpus_vocab.md exists and embodies G1–G3 structurally (entry-test, entry-shape, firmness taxonomy). G4 (firmness asymmetry: operational-substrate vs. ratified-corpus firmness) and G5 (disambiguation rules-out vs. conviction rules-out) are structural arguments for *how to read* corpus_vocab.md that never landed as §-claims. Agents reading corpus_vocab.md without G4/G5 can collapse the two firmness levels or misread the disambiguation function. Needs its own ratification pass.

**C3. Epistle-022 (Telos as Zeroth-Class Artifact) — warrant never ratified.** telos.md exists and instantiates the zeroth-class structure (off the §1.12 scale, prior to the spine, no arrow pointing out). The three arguments for why telos deserves zeroth-class status — inverted-ratifiability test, prayer as distinct speech act, pre-justified container — were never staked as §-claims. The artifact landed; the warrant is oral tradition. §13 is the right home (epistemic frame); the specific §-address is open. Needs its own ratification pass.

**C4. Epistle-025 (Four Causes, Four Faults) — most gold never ratified.** Four claims that did not land: the Aristotle-grounding-inversion (the four causes are not a flat taxonomy — §13.6 absorbed this partially but the inversion was staked more sharply in 025); §1.12 confirmed-independently-rather-than-derived (the intent spine is independently confirmed by the four-cause analysis, not derived from it); causal-interaction-as-prediction-not-coincidence; telos/fault duality. "fault" is not in corpus_vocab.md. §8.12 leaves the orthogonal-vs-ordered tension open (whether the four primitives are causally independent or share a root) — epistle-025 had a position on this that was not ratified. Needs its own ratification pass.

Epistles C1–C4 are not housekeeping. They require the shitcorping loop: lite pans against live corpora, author responds, builder commits. Named here so the gap is queryable; do not close by assumption.

---

**A note on scope.** A1–A9 are defects: wrong names, phantom citations, inverted order, one-line errors. They land on ratification of this epistle — housekeeping commits. B1 is a genuine stake: a new §-claim addressing a phantom citation the corpus has been carrying. C1–C4 are deferred ratification events, not housekeeping — they require full shitcorping passes and are named here as the queue.

[→ §1.12, §1.16, §2.5, §3.20, §6.6, §13.6, §15.17, §15.18, §17.1, §17.4, telos.md, corpus_vocab.md, process.md, rhetoric.md §4.2, Epistle 013, Epistle 014, Epistle 022, Epistle 025, Epistle 032]
