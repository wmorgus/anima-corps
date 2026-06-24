# System State — 2026-06-22

**Session history:** `session-log.md` (sessions 1–7 chronological log, preserved)
**Purpose:** current open gaps + next queue; updated as gaps close or open

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
| ~~Semantic search disabled~~ | ~~**Blocking**~~ | ~~CLOSED 2026-06-22~~ — Python cosine fallback (local dev), OpenAI embedder injected via env, 725 artifacts backfilled. |
| §1.12 type expansion | Medium | Contract, operational, verification registers. Derive from §1.12, not pipeline. Epistle 048 stakes this. |
| `deployment_record` schemaless | Low | Enum-present, no `_CONTENT_SCHEMAS` entry |
| `field_provenance_ancestors` stub | Low | Traversal preset returns empty |
| Graph traversal unused by agents | Low | `traverse()`, `lineage()`, `impact()` exist on CalliopeClient and are exposed as tools — agents never reach for them. `relates_to` and `parent_artifact_id` edges are never walked at runtime; only `supersedes` is followed (auto via `follow_supersession=True`). Gap is behavioral: no agent prompt or retrieval pattern prompts structural traversal. Semantic search is the default; graph is an afterthought. |
| Manifest upsert ID collision | Low | Successor manifest ID collides on re-run |
| 2 cross-repo integration tests skipped | Low | Require `hermes` package or external `DECISIONS.md` |

### aZero

| Gap | Severity | Notes |
|-----|----------|-------|
| Face enforcement — explicit triggers enforced, default face open | Low | **Partially closed 2026-06-23:** `HermesAgent.run()` now detects face trigger keywords (`builder`, `lite`, `shitcorp`, etc.) and calls `load_face` programmatically before first LLM turn. 24 tests. **Remaining open:** (1) untagged tasks have no default face — model still decides via advisory prompt; (2) §6a.5 advisory instructions still in `agent-prompt-hermes-001` (cleanup deferred — separate corpus authoring task); (3) no "default to builder for all prose/authoring tasks" policy — intentional deferral pending design call. |
| Agent prompt schema drift | Medium | Hermes/Clio prompts are legacy; `dk-calliope-schema-v2-001` helps but enforcement is prompt-level only |
| ~~Urania produces no build_verification artifacts~~ | ~~Medium~~ | **CLOSED 2026-06-23** — surgical tools (`search_file`, `read_file_section`) implemented with ANIMA_WORKSPACE_ROOT scope; `build_verification` schema block added to `agent-prompt-urania-001`; evidence anchor changed from `pull_request` to sprint_contract; `cites` required field documented. Loop should now close. Needs end-to-end dogfood test to confirm. |
| `spawn_swarm` executor never built | Medium | Telescoping not functional — inherited gap |
| `MnemosyneAgent.__init__` blocking sync I/O | Medium | Needs `begin_session()` async pattern before wired into daemon |
| `on_pr` / `on_artifact` daemon triggers stubbed | Low | Require Calliope event subscription |
| `web_search` stub | Low | No backend |
| Cross-restart sweep dedup | Low | Sweep artifacts written but not consulted on restart |

### Corpus / retrieval

| Gap | Severity | Notes |
|-----|----------|-------|
| ~~Index artifacts — not designed~~ | ~~**Precondition**~~ | ~~CLOSED 2026-06-22~~ — Epistle 050 frozen: `corpus_index` type, summary+claims shape, §2.11/§4.10/§6.13b in corpus, process.md step 6 added. |
| Chunking + semantic retrieval | Blocked | #1 self-directed task. Blocked on: (a) ~~embedder in Calliope~~ ✓, (b) ~~Index artifact design~~ ✓. Next: implement `corpus_index` type in Calliope + Mnemosyne generation step. |
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

1. ~~**Semantic search + embedder**~~ — CLOSED 2026-06-22
2. ~~**Index artifact design**~~ — CLOSED 2026-06-22 (Epistle 050)
3. ~~**`corpus_index` type + Mnemosyne generation**~~ — CLOSED 2026-06-23 (Heph via dogfood loop; `corpus_index` in types.py, CorpusIndexContent schema, lifecycle hooks in service.py, corpus_index.py)
4. ~~**Face enforcement (explicit triggers)**~~ — CLOSED 2026-06-23 (interception layer in HermesAgent.run(); 24 tests; default-face policy and §6a.5 cleanup still open, documented in gaps table)
5. ~~**Urania build_verification**~~ — CLOSED 2026-06-23 (surgical tools, schema, evidence anchor)
6. **Dogfood loop end-to-end test** — run a real sprint through Hermes→Clio→Heph→Urania and confirm `build_verification` closes; first full loop closure
7. **§1.12 type expansion** — contract/operational/verification registers (Epistle 048 stakes this; epistle track)
8. **corpus_index backfill** — generate corpus_index artifacts for the 50 existing frozen corpus_sections (Mnemosyne step)
9. **Default face policy** — should untagged prose/authoring tasks default to builder? Design call before implementation

---

## Open tensions (from Epistle 039)

1. **Multi-device / CC-plugin delivery** — §4.7 / Epistle 031. Surfaces by build pressure.
2. **Discipline-boundary cost of unification** — discipline lives in Calliope + ratification process, not repo boundary.
3. **CORPS_VERSION fate** — dissolves or transforms into "ratified-against" marker.
