# System State — 2026-06-22

**Supersedes context from:** `build-tracker.md` (sessions 1–7 log, preserved)
**Purpose:** clean forward-looking state doc; build-tracker.md is the historical record

---

## What's live

### Calliope — localhost:8100
- 450 tests passing (2 skipped)
- Freeze step live
- Types: full enum, typed content models for all priority types; `agent_prompt` type (Epistle 048)
- Corpus: 50 corpus_section artifacts + corpus_manifest (anima corpora)
- Constellation: 6 agents migrated from calliope_legacy (Option A); all agent_prompt artifacts
- Epistles 038, 039, 045, 046, 047, 048 frozen
- §6.12d frozen (first dogfood corpus output)
- `ingest_anima_corpora.py` upserts on re-run

### aZero — 78 tests passing
- Library + daemon (Epistle 038)
- All 6 agents: gpt-5.5/openai except Heph (anthropic/claude-sonnet-4-6)
- Editor tools: write_file, edit_file, run_command, glob_search, grep_search — real implementations
- `load_face` tool: FaceValidator, CallioPeFaceRepository, structured failures, audit records (sc-azero-load-face-007)
- `prompt-builder-002` + `prompt-lite-002`: agent_prompt with FaceArtifact fields; load_face("builder"/"lite") → LoadFaceSuccess verified
- Hermes→Clio→Heph loop proven; sprint contracts authoring through the system

### anima-corps
- Epistles 042–048 authored and shitcorped
- process.md: freeze procedure updated — 5-step sequence with Calliope sync steps
- substrate.md: §6.12d added

### Bench — not started

---

## Open gaps

### Calliope

| Gap | Severity | Notes |
|-----|----------|-------|
| Semantic search disabled | **Blocking** | `search_artifacts` fails on every agent run — embedder not injected into ArtifactService. Blocks Hermes/Clio from finding artifacts by content. |
| §1.12 type expansion | Medium | Contract, operational, verification registers. Derive from §1.12, not pipeline. Epistle 048 stakes this. |
| `deployment_record` schemaless | Low | Enum-present, no `_CONTENT_SCHEMAS` entry |
| `field_provenance_ancestors` stub | Low | Traversal preset returns empty |
| Manifest upsert ID collision | Low | Successor manifest ID collides on re-run |
| 2 cross-repo integration tests skipped | Low | Require `hermes` package or external `DECISIONS.md` |

### aZero

| Gap | Severity | Notes |
|-----|----------|-------|
| Face enforcement missing | Medium | gpt-5.5 skips `load_face` call for pure text tasks — MUST instruction advisory, no code-level enforcement. Face section in Hermes startup prompt is §6a.5 startup injection (contradicts Epistle 047). Fix: interception layer + remove face content from startup prompt. |
| Agent prompt schema drift | Medium | Hermes/Clio prompts are legacy; `dk-calliope-schema-v2-001` helps but enforcement is prompt-level only |
| Urania produces no build_verification artifacts | Medium | Governance gate doesn't close after Heph builds |
| `spawn_swarm` executor never built | Medium | Telescoping not functional — inherited gap |
| `MnemosyneAgent.__init__` blocking sync I/O | Medium | Needs `begin_session()` async pattern before wired into daemon |
| `on_pr` / `on_artifact` daemon triggers stubbed | Low | Require Calliope event subscription |
| `web_search` stub | Low | No backend |
| Cross-restart sweep dedup | Low | Sweep artifacts written but not consulted on restart |

### Corpus / retrieval

| Gap | Severity | Notes |
|-----|----------|-------|
| Index artifacts — not designed | **Precondition** | Entry-point artifacts per corpus section required before effective chunking+retrieval. Shape TBD: summary+claims list, tag cloud, Q&A pairs? |
| Chunking + semantic retrieval | Blocked | #1 self-directed task. Blocked on: (a) embedder in Calliope, (b) Index artifact design. Both halves only pay off together. |
| Corpus citation §-number location confusion | Medium | §-numbers travel with claims across corpus migrations; causes reader confusion about file-of-residence. Queue for corpus tooling sprint. |
| §6a.6 still open | Low | git corpus and Calliope disagree on closure. Must close in Calliope first when it closes. |

### Process / governance

| Gap | Severity | Notes |
|-----|----------|-------|
| Epistles 042, 043 not frozen in Calliope | Low | Written and shitcorped; full 5-step freeze procedure now defined but not yet run on these |
| 038 ratification fork | Low | Gold 2 (§6a.10 pull primitive) or gold 4 (§1.5 server role-shedding) may warrant VERSION minor bump + corpus amendment. Human call. |
| CORPS_VERSION fate | Low | Dissolves or becomes "ratified-against" marker. Surfaces by build pressure. |
| Multi-device / CC-plugin delivery | Low | aZero as CC plugin; multi-host `asserted_by` provenance (§4.7 / Epistle 031). Surfaces by build pressure. |

---

## Next queue (priority order)

1. **Semantic search + embedder** — inject embedder into ArtifactService; unblocks Hermes tool surface and is prerequisite for chunking
2. **Index artifact design** — what shape? epistle track or design session?
3. **Chunking + semantic retrieval** — chunk corpus per-§, add semantic retrieval to base.py
4. **Face enforcement** — code-level load_face check; remove face from Hermes startup prompt
5. **Urania build_verification** — why Urania doesn't emit verification artifacts
6. **§1.12 type expansion** — contract/operational/verification registers

---

## Open tensions (from Epistle 039)

1. **Multi-device / CC-plugin delivery** — §4.7 / Epistle 031. Surfaces by build pressure.
2. **Discipline-boundary cost of unification** — discipline lives in Calliope + ratification process, not repo boundary.
3. **CORPS_VERSION fate** — dissolves or transforms into "ratified-against" marker.
