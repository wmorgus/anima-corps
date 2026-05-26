---
Excavated: 2026-05-24 | Status: liquid
---

Epistle 006 — File as View
Topic: When a Calliope artifact has a canonical human-readable file expression, Calliope is the source of truth and the file is a derived view. Inversion is the failure mode behind three §6a contradictions.

§6a names three contradictions that look distinct and aren't. 6a.6 — frozen corpora invisible to runtime agents (corpus_logic.md lives in `docs/papers/`, no agent can retrieve it). 6a.7 — decorative liquidity tags on prompt files outside Calliope (the tag satisfies §2's form without §4.2's substrate). 6a.8 — mutable frozen artifact (`builder_philosophy.md` carries `liquidity: frozen` while remaining a git-editable file, violating §3.10's supersession-only rule). One root: the file is currently the source of truth and the Calliope artifact is absent, ghost, or downstream. Inverted.

Stake: file-as-view. A Calliope artifact may have a canonical human-readable expression — a markdown file checked into git, readable by humans without an agent in the loop. The file is a view over the artifact, not the artifact itself. The artifact carries the liquidity tag, the citations, the supersession chain, the `asserted_by`. The file renders some of that, formatted for human reading. The artifact is governance-bearing; the file is display.

Files don't disappear. Readability survives. What changes is the direction of authority: edit the artifact through supersession (§3.10, §4.3), regenerate the view. Edit the view directly and the artifact is unchanged — meaning the edit has not happened in any load-bearing sense. Two registers, one source.

The inversion test. Can a change to the file fail to appear in Calliope? If yes, the file is the source of truth. That is the 6a.8 failure mode named operationally. A `git commit` to corpus_logic.md that produces no Calliope artifact is the test failing — the corpus updated, the substrate didn't, and §17.1 ("updates are supersession events") is satisfied in name only.

Consistency guarantee — who regenerates the view? Two candidate mechanisms, neither yet specified.
(a) Automatic. Calliope emits an event on supersession; a registered hook regenerates the file from the new artifact and writes it to the working tree (or to a build output). Infrastructure-heavy: hook registry, render templates per artifact_type, working-tree write authority. The guarantee is structural — drift is impossible by construction.
(b) Manual. The ratification cycle requires file regeneration as part of the supersession act. The supersession artifact's `cites` includes a `view_regenerated` reference (or the act is incomplete). Governance-heavy: discipline-bearing, contestable at ratification time, no infrastructure required. The guarantee is procedural — drift is detectable but not prevented.

Don't pick yet. Both are admissible. The choice has consequences for §15.2 (prompts-as-artifacts) and for whatever rendering registers §18 ends up requiring at the artifact layer.

What this resolves. If corpus_logic.md is a view over a Calliope artifact, 6a.6/6a.7/6a.8 dissolve together. The file stays in git for human readability — that is the view's job. The liquidity tag on the file becomes a rendered display of the artifact's tag, not a free-floating decoration; the tag is operative at the artifact, decorative-but-honest at the view. The frozen-mutable contradiction collapses: the artifact is frozen and supersession-only; the file is regenerable and therefore not in epistemic tension when it changes. The edit-the-file-to-update-the-corpus pattern is named as the inversion it is.

→ tensions
- Files without Calliope counterparts. Notes, drafts, prompt files, queue READMEs — are they ungoverned views (allowed, but no governance claim attaches) or prohibited (every readable file must trace to an artifact)? Both readings have costs. Prohibition demands a Calliope artifact for every readable file in the repo, which the substrate cannot yet carry. Permission opens a back door: ungoverned files accumulate authority through being read. Don't know yet.
- Bootstrap. The file-as-view model requires the Calliope artifact to exist. Right now corpus_logic.md *is* the artifact in practice — there is no upstream. Instantiating the corpus_logic artifact in Calliope is the prerequisite move, and §16 territory: a known gap with no current implementation surface. Until the artifact exists, the inversion test cannot be run.
- Consistency mechanism underspecified. Automatic regeneration needs render templates per artifact_type and a hook system the substrate does not have. Manual regeneration needs ratification-cycle discipline that names view regeneration as part of the supersession act — which means amending §3 or §4 to carry it. Neither path is free; the choice is a real architectural commitment, not an implementation detail.
- View fidelity. A view is a projection. Two artifacts cannot render to the same file without collision; one artifact may render to multiple views (full corpus, summary, agent-context slice). The mapping is one-to-many artifact→view, and the canonical view (the one the file represents) needs a name. Unspecified.
- §15.2 relationship. Prompt files are the same problem in a different domain — the prompt is currently the source of truth, no Calliope artifact upstream. File-as-view is the structural answer for both, but §15.2 also waits on §15.8 (naming the evaluative bedrock the prompts encode). The view model unblocks the substrate question without closing the bedrock question. Partial overlap, not identity.
- §17 status. §17.1 commits to this corpus being a frozen artifact updated by supersession. The current implementation (git-edit the markdown) does not satisfy that commitment. This epistle, if it survives excavation, makes the gap impossible to ignore. §17 is sui generis per §18.5 and may need amendment to carry the file-as-view distinction explicitly.
- Vapor; excavation pending.
