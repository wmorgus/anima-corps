# Build Tracker — One Home Transition

**Last updated:** 2026-06-22 (session 7 close)
**Supersedes:** previous build-tracker.md (sessions 1–7 log)

One Home Transition: nuclear rebuild of Calliope, aZero, anima-corps, Bench in dependency order. No incremental migration.

---

## System state (as of 2026-06-22)

### Calliope — live at localhost:8100
- Built, 450 tests passing (2 skipped)
- Freeze step implemented and proven
- Types: full enum, typed content models for all priority types
  - Includes `agent_prompt` (Step 0, Epistle 048) — §1.12 prompt-as-artifact register
- Corpus ingested: 50 corpus_section artifacts + corpus_manifest
- Constellation migrated from calliope_legacy (Option A): 6 agents, all agent_prompt artifacts
- Epistles 038, 039, 045, 046, 047, 048 frozen in Calliope
- §6.12d corpus_section frozen (first dogfood corpus output)

### aZero — CLI gate, 78 tests passing
- Library + daemon shape (Epistle 038)
- All 6 agents with gpt-5.5/anthropic correct providers
- Editor tools implemented: write_file, edit_file, run_command, glob_search, grep_search
- `load_face` tool built (Hephaestus, sc-azero-load-face-007, 22 tests)
- Hermes→Clio→Heph dogfood loop proven; sprint contracts authoring through the system
- `prompt-builder-002` + `prompt-lite-002`: agent_prompt type with FaceArtifact fields; load_face("builder"/"lite") → LoadFaceSuccess verified

### anima-corps — authoring surface
- Epistles 042–048 authored and shitcorped
- process.md: freeze procedure updated with Calliope sync steps (5-step sequence)
- substrate.md: §6.12d added (face generalization, intake-depth axis)
- ingest_anima_corpora.py: upserts on re-run (batch → per-item)

### Bench — not started
Depends on aZero being stable.

---

## Open gaps

### Calliope

| Gap | Severity | Notes |
|-----|----------|-------|
| Semantic search disabled | **Blocking** | `search_artifacts` fails on every agent run — embedder not injected into ArtifactService. Blocks Hermes/Clio from finding artifacts by content. |
| §1.12 type expansion | Medium | Contract registers (API contracts, data schemas, event schemas, permission schemas, SLAs), operational registers (runbooks, deployment manifests, config, feature flags), verification registers (security audits, benchmarks). Design criterion: derive from §1.12, not pipeline. Epistle 048 stakes this. |
| `deployment_record` schemaless | Low | Enum-present but no `_CONTENT_SCHEMAS` entry — name without schema |
| `field_provenance_ancestors` stub | Low | Traversal preset returns empty |
| Manifest upsert ID collision | Low | `ingest_anima_corpora.py` successor manifest gets ID collision on re-run |
| 2 cross-repo integration tests skipped | Low | Require `hermes` package or external `DECISIONS.md` |

### aZero

| Gap | Severity | Notes |
|-----|----------|-------|
| Face enforcement missing | Medium | gpt-5.5 skips `load_face` call for pure text tasks — MUST instruction advisory, no code-level enforcement. Face section added to Hermes prompt is startup injection (§6a.5 violation, contradicts Epistle 047). Real fix: interception layer before corpus text output on named-face tasks + remove face content from startup prompt. |
| Agent prompt schema drift | Medium | Hermes/Clio prompts are legacy (45KB+). They know about `load_face` and Calliope v2 schema via DK but occasionally generate wrong field names or missing required fields. `dk-calliope-schema-v2-001` helps but not complete. |
| Urania produces no build_verification artifacts | Medium | Seen in Heph build run — Urania ran but emitted no verification artifact. Governance gate doesn't close. |
| `spawn_swarm` executor never built | Medium | Inherited gap from legacy. Telescoping not functional. |
| `MnemosyneAgent.__init__` blocking sync I/O | Medium | MCP server startup blocks — needs `begin_session()` async pattern before Mnemosyne wired into daemon |
| `on_pr` / `on_artifact` daemon triggers stubbed | Low | Require Calliope event subscription |
| `web_search` stub | Low | No backend |
| Cross-restart sweep dedup | Low | Sweep artifacts written but not consulted on restart |
| routing_decision content sometimes wrong | Low | Hermes sometimes writes wrong fields — DK has schema but enforcement is prompt-level only |

### Corpus / retrieval

| Gap | Severity | Notes |
|-----|----------|-------|
| Index artifacts — not yet designed | **Precondition** | Entry-point artifacts per corpus section required before effective chunking+retrieval. Needs design pass (what shape: summary+claims, tag cloud, Q&A pairs?). |
| Chunking + semantic retrieval | Blocked | #1 self-directed task. Blocked on: (a) semantic search embedder in Calliope, (b) Index artifact design. Both halves pay off together. |
| Corpus citation system gap | Medium | §-numbers travel with claims across migrations (logic→substrate per §32); causes reader confusion about file-of-residence. Queue for corpus tooling sprint. |
| §6a.6 open | Low | git corpus and Calliope disagree on whether it's closed. When it closes, must close in Calliope first. |

### Process / governance

| Gap | Severity | Notes |
|-----|----------|-------|
| Epistles 042, 043 not yet frozen in Calliope | Low | Written and shitcorped; full freeze procedure now defined but not yet run on these |
| 038 ratification fork | Low | If gold 2 (§6a.10 pull primitive) or gold 4 (§1.5 server role-shedding) is ratification-grade, requires VERSION minor bump + corpus amendment. Human call. |
| CORPS_VERSION fate | Low | Dissolves under single source of truth, or transforms into "ratified-against" marker? Surfaces by build pressure. |
| Multi-device / CC-plugin delivery | Low | aZero as CC plugin; multi-host `asserted_by` provenance (§4.7 / Epistle 031). Surfaces by build pressure. |

---

## Next queue (priority order)

1. **Semantic search + embedder** — inject embedder into ArtifactService; unblocks Hermes tool surface and is prerequisite for chunking
2. **Index artifact design** — what shape? epistle track or design doc? precondition for chunking
3. **Chunking + semantic retrieval** — chunk corpus per-§, add semantic retrieval to base.py; only pays off with (1) and (2)
4. **Face enforcement** — code-level load_face check; remove face from Hermes startup prompt
5. **Urania build_verification** — why Urania doesn't emit verification artifacts
6. **§1.12 type expansion** — contract/operational/verification registers

---

## Open tensions (from Epistle 039)

1. **Multi-device / CC-plugin delivery** — §4.7 / Epistle 031. Surfaces by build pressure.
2. **Discipline-boundary cost of unification** — discipline lives in Calliope + ratification process, not repo boundary. Real cost, not waved away.
3. **CORPS_VERSION fate** — dissolves or transforms into "ratified-against" marker. Surfaces by build pressure.
