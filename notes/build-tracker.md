# Build Tracker — One Home Transition

**Sourced from:** `notes/one-home-transition.md`
**Started:** 2026-06-16
**Last updated:** 2026-06-18 (session 5)

---

## The plan (formalized)

Nuclear rebuild. No incremental migration. Four projects in dependency order:

1. **Calliope** — governed artifact store. Telos: externality primitive that makes §3.3 real. No upstream Anima dependencies; everything else depends on it.
2. **aZero** — faithful CLI implementation. Library + daemon shape (Epistle 038). The seam that puts §4 discipline behind one wall.
3. **Bench** — rich human-facing UI. Invokes aZero; talks to Calliope directly.
4. **anima-corps** — authoring surface. Stays as git corpus; ratifies INTO Calliope once freeze step exists.

Committed-for-build architecture (liquid, not yet ratified): Epistles 038, 039, 040, 041.

038/039 ratification held deliberately — they freeze into the new world once Calliope's freeze step exists. Not frozen under the old process.

---

## Calliope build

### Decisions staked (2026-06-16)

| # | Decision |
|---|---|
| 1 | Library first, server optional (`calliope.server` subpackage) |
| 2 | Embedder injection — `ArtifactService.__init__` accepts `embedder: Callable | None` |
| 3 | Domain exceptions — `CalliopePermissionError` etc., not `HTTPException` |
| 4 | Reconcile two `types.py` files — calliope-anima base + anima-core field additions |
| 5 | `artifact_versions`: archive before minor mutations (`update_review_status`, `update_links`) |
| 6 | External registry / filesystem tracking — **pinned future direction, out of scope for this pass** |
| 7 | Freeze authority — human always; agent only if `review_status=="approved"` pre-existing |
| 8 | Freeze does not auto-emit ratification record — caller (Hermes/human) writes `ARCHITECTURAL_DECISION` citing the frozen artifact |

Source selected: `calliope-anima/api/artifacts/` (Implementation A) over `anima-core/src/anima_core/calliope/` — A has `RevisionRequestContent` + closure-on-supersede logic; B does not.

MongoDB confirmed (not Postgres — `ARCHITECTURE.md` in calliope-anima is a fossil).

### Location
`~/Desktop/anima/calliope/` — joins the umbrella.

### Status

- [x] Shell created — `telos.md`, `CLAUDE.md`, `src/calliope/__init__.py`, `tests/__init__.py`
- [x] Archaeology pass completed — inheritance manifest produced (see session notes)
- [x] First-pass rebuild complete — **433 passed, 2 skipped, 0 failures**
- [x] Code review pass — 11 findings surfaced (7 bugs/structural, 4 design gaps)
- [x] Fixes 1–7 applied — **433 passed, 2 skipped, 0 failures**
  - `AgentIdentity` moved to `calliope/identity.py` (FastAPI leak eliminated)
  - `fastapi` removed from core deps (optional `[server]` only)
  - `archive_version` duplicate key fixed (timestamp suffix)
  - `find_live_successor` sort fixed (`created_at` desc, not `_id` desc)
  - Successor ID generation fixed (strips `-vN` suffix before incrementing)
  - `store.client` property added; `_col` private access removed from service
  - `background_tasks` FastAPI coupling removed from service; `flagged_dependent_ids` on `ArtifactResponse`
- [x] Fixes 8–11 applied — **433 passed, 2 skipped, 0 failures**
  - 8: `ArtifactUpdate` constraint documented (no `cites`/`edges` on supersession — audit legibility)
  - 9: `_create_conflict_records` populates `cites` with conflicting artifact IDs
  - 10: `update_links` add/remove wrapped in Motor session
  - 11: `Liquidity` enum normalization in `service.update` (defensive, string vs. enum)
- [x] Git init + first commit — `038b7d0` (42 files, 11,590 insertions)
- [x] Freeze step implemented — **450 passed, 2 skipped, 0 failures**
  - `store.freeze_artifact` — archive → atomic `liquidity=frozen` + `review_status=approved`
  - `service.freeze` — authority check + corpus audit closure + dependent flagging
  - `POST /artifacts/{id}/freeze` router endpoint
  - 17 new tests (`tests/test_freeze.py`), 3 classes: service / store / HTTP
- [x] aZero archaeology pass completed — inheritance manifest produced (`notes/azero-inheritance-manifest.md`)
  - Live Calliope survey: 305 sprint contracts, 218 build decisions, 65 architectural decisions, 228 domain_knowledge artifacts
  - Codebase survey: anima-core structure, all 26 drive scripts, six agent classes, server layer fractures
  - Cross-corroborated: Hermes merge (May 25), pure-append semantics live, constellation cites context live
- [x] New Calliope stood up — server running on port 8100, `calliope_legacy` preserves old data
- [x] Calliope types.py — add `corpus_section`, `corpus_manifest`, `epistle`, `gravel_record` (defined by Epistle 043)
- [x] Re-ingest anima corpora as `corpus_section` artifacts — 50 sections + corpus_manifest in Calliope
  - aZero not yet in substrate.md: 038 must be frozen first; substrate coverage marked `in_progress` in manifest
- [x] Seed `anima` project — 038 (liquid) + 039 (semi_liquid) as `epistle` artifacts
- [x] 038 ratification — frozen, approved, version=1
- [x] 039 ratification — frozen, approved, version=1

### Design decisions made during review

- `ArtifactUpdate` intentionally excludes `cites`/`edges` — supersession and relationship assertions are separate acts; conflating them ambiguates the audit record. Callers add new edges via links PATCH on the successor.
- `_create_conflict_records` cites the conflicting artifacts (correct semantic, not a bypass).

### Known gaps / deferred

- `field_provenance_ancestors` traversal preset is a stub (returns empty) — queued as future item
- 2 cross-repo integration tests skipped (require `hermes` package or external `DECISIONS.md`)
- External registry / filesystem tracking (pinned — own work item when ready)

---

## Corpus shape work (session 5, 2026-06-18)

### Epistles written and shitcorped

**Epistle 042 — The Iceberg: Dojo In, Forge Out** (semi-liquid)
- Coins dojo (surface → Calliope) and forge (Calliope → surface) as the two faces of the efficient cause
- Three surface types: authored doc (dojo-primary), generated doc (pure-forge, no dojo path), code
- Diagnoses domain_knowledge overload as the unnamed-forge asymmetry
- Open tension T1: the forge has no externality cut yet (candidate for own epistle)

**Epistle 043 — The Corpus Has No Type** (semi-liquid)
- Defines `corpus_section` (section-granular, frozen, human_only ratification)
- Defines `corpus_manifest` (four-cause coverage instrument, enforced at completeness declaration)
- Defines `epistle` and `gravel_record` as Calliope-native provenance types; smith_notes as optional field on gravel_record
- Ari reads the manifest; his telos authority is the mechanism that makes four-cause coverage reachable

### Design decisions staked

- **Bench's telos = Anima's efficient cause instantiated** — a project's final cause can be a system-level cause role
- **Iceberg model** — every project has canonical Calliope body + human-visible surfaces; doc surfaces have dojo+forge; generated docs are pure-forge
- **Re-ingest over port** — legacy data under `calliope_legacy`; fresh ingest against new types once types.py is updated

### Next actions
1. Calliope types.py — implement `corpus_section`, `corpus_manifest`, `epistle`, `gravel_record`
2. Re-ingest anima corpora as `corpus_section` artifacts into new Calliope
3. Seed 038/039 as liquid `epistle` artifacts → ratify via freeze step

---

## aZero build

**Status:** Initial build complete. 36 tests passing. `c98dd33`.

**Telos doc:** `aZero/telos.md` — written via G1 Moves 1+2 (2026-06-18). Gate metaphor ratified. Telos: put §4 discipline behind one gate; any caller crosses it by shelling `anima`.

**Shape (from Epistle 038):** Library + daemon. Hosts own the HTTP surface; aZero is the CLI.

**Inheritance manifest:** `notes/azero-inheritance-manifest.md`

### Build complete (2026-06-18)

- [x] Telos doc written + ratified (`aZero/telos.md`)
- [x] G1 Epistle 041 sequence run — four stories proven:
  - S1 ✓ gate holds for any caller (universal CLI entry point)
  - S2 ✓ §4 enforced structurally (no bypass path to Calliope)
  - S3 ✓ triggering is live, not compiled (Hermes dispatches via tools)
  - S4 ✓ daemon outlives its host (host-neutral asyncio lifecycle)
- [x] lib/ core — CalliopeClient (HTTP, not in-process), BaseAgent, providers, cost, trace
- [x] lib/agents/ — all six agents, FastAPI stripped, UraniAgent → UraniaAgent
- [x] lib/tools/ — dispatch, relay, probe_events, shitcorpus, web (web_search stubbed)
- [x] cli/ — thin gate shell, Click, relay open/close, correct crossing_index
- [x] daemon/ — on_load + on_cron fully implemented; on_pr + on_artifact stubbed
- [x] 36 behavioral tests passing (4 code review passes applied)
- [x] Committed — `c98dd33`

### Known gaps / deferred

- `MnemosyneAgent.__init__` blocking sync I/O (MCP server startup) — needs `begin_session()` async pattern before Mnemosyne is wired into daemon
- `spawn_swarm` executor still never built (inherited gap)
- `web_search` stub (no backend — inherited gap)
- Calliope graph retrieval flat/lexical (inherited gap)
- Pavel §6.14 OPEN (inherited gap)
- Cross-restart sweep deduplication — sweep artifacts written but not consulted on restart
- `on_pr` / `on_artifact` daemon triggers stubbed (require Calliope event subscription)

---

## Face mechanism + dogfood (session 7, 2026-06-22)

**Status:** Doctrine staked. Build not started.

### Doctrine ratified (all frozen in Calliope)

- **Epistle 045** (`anima-epistle-045`) — face is configuration, not an agent; intake-depth axis on Hermes; §6.12a extension (amendment-track); builder/lite as faces via §6.1 information-poet harm test
- **Epistle 046** (`anima-epistle-046`) — builder+lite missed in aZero initial build; last hand-authored epistle; `prompt-builder-001` + `prompt-lite-001` seeded in Calliope as `domain_knowledge`
- **Epistle 047** (`anima-epistle-047`) — load_face mechanism: face selection by live Hermes reasoning (§6.0/§15.18, not §6.12b); §6a.10 pull from Calliope at task time; §5.4 forbids invisible re-assertion; §6.1 harm test run (builder/lite = faces, not slots)

### Key design decisions

- Face = persona + intake-depth config on Hermes, pulled from Calliope at task time
- `load_face(face_id)` tool — new, does not exist yet; fetches `domain_knowledge` artifact, returns `full_text`
- `_ensure_context_loaded` is startup-cached (§6a.5 shape) — face-pull is NEW machinery, not the existing cites path
- `--face` flag valid for programmatic callers (Slack); primary path is live Hermes reasoning
- `agent_prompt` type does not exist in Calliope schema — 045 open (prompt-* vs dedicated type) still open
- builder/lite stay as faces (not constellation entries) — §6.1 returns information-poet harm, same as §11/Ari

### Next actions (pinned)

**Prerequisite fork — choose before building:**

**Option A — migrate constellation first, then full dogfood**
1. Port constellation + agent prompts from `calliope_legacy` (port 27017) to new Calliope (port 8100)
2. Write sprint contract for load_face feature → Clio plans → Heph builds in aZero
3. Test `anima "write this up with builder"` → Hermes loads builder face → corpus amendment

**Option B — direct Heph dogfood, skip constellation for now**
1. Write sprint contract for load_face manually, seed into new Calliope
2. Invoke HephaestusAgent directly (drive script pattern via aZero) to build load_face
3. Proves build loop works; full Hermes + faces wiring comes after

**After load_face is built (both paths):**
- 045 corpus amendment: amend `substrate.md` §6.12a (add face extension), create superseding `corpus_section` in Calliope, freeze — first real output of dogfood loop

---

## Bench build

**Status:** Not started. Depends on aZero.

**Telos:** Rich human-facing interface — the VS Code fork where human and Anima work together.

**Base:** `anima-bench/` (existing claw-code/Claude Code foundation).

### UI notes

- **§ citation popovers** — in certain views, hovering over a §1.5-style citation should show a popover with the cited text. Scope TBD (corpus views likely; not all views).

---

## Open tensions (from Epistle 039, not resolved)

1. **Multi-device / CC-plugin delivery** — aZero as a Claude Code plugin riding CC-as-host; multi-host `asserted_by` provenance (§4.7 / Epistle 031). Surfaces by build pressure.
2. **Discipline-boundary cost of unification** — repo boundary previously enforced corpus vs. code discipline crudely. Resolution: discipline lives in Calliope + ratification process, not repo boundary. Real cost, not waved away.
3. **CORPS_VERSION fate** — dissolves under single source of truth, or transforms into a "ratified-against" marker? Surfaces by build pressure.

---

## Verification flags (from one-home-transition.md)

- **§6a.6 still open** — git corpus and Calliope state disagree on whether it's closed. Standing TODO: when §6a.6 closes, it must close in Calliope (the real fix), and git corpus must reflect it. Test case for the freeze→Calliope propagation (039 claim 2).
- **038 gravel corrected** — both originally-proposed tensions dissolved. Record shows no open tensions. Read corrected `gravel/epistle-038.md` if 038 moves toward ratification.
- **038 ratification fork** — if gold 2 (seam as §6a.10 pull primitive) or gold 4 (§1.5 server role-shedding) is ratification-grade, that is a separate event requiring VERSION minor bump + corpus amendment. Human call. Should use new freeze step.
