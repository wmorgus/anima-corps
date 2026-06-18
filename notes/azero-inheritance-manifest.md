# aZero Inheritance Manifest

**Source:** archaeology of anima-core (`src/anima_core/`) + live Calliope survey (MongoDB `localhost:27017`, db `calliope`)
**Date:** 2026-06-16
**Purpose:** governed sort for the aZero rebuild (One Home Transition). What carries, what dies, the because for each call.

---

## Inherits

| Item | Source | Why it carries |
|------|--------|----------------|
| `BaseAgent` agentic loop | `src/anima_core/agents/base.py` | `run()`, `stream()`, tool execution, cost tracking, trace recording — none of it touches FastAPI. It is a pure async loop over a Provider. The server wraps it; it does not depend on the server. |
| `_ensure_context_loaded` (cited-context loader) | `src/anima_core/agents/base.py:96` | Fetches `anima-constellation-current`, reads the agent's `cites` list, pulls each cited artifact in order. Identity is configuration — the pattern doesn't care whether the caller is a server or a CLI. Confirmed live per `sc-base-agent-calliope-context-001`. |
| `Provider` protocol + three backends | `src/anima_core/providers/base.py`, `anthropic.py`, `openai.py`, `ollama.py` | Normalizes `call`/`stream` across providers. Tool schema conversion (Anthropic ↔ OpenAI) lives in the provider layer. No server dependency anywhere in the provider tree. |
| Tool definition/handler factory pattern | All `tools/` modules | `TOOL_DEFINITION` dict + `make_*_handlers(calliope)` factory. Composable, resource-closed at construction. The pattern is the right surface shape for aZero — compose a tool surface from capability modules, pass a Calliope handle. |
| `HephaestusAgent` build machinery | `src/anima_core/agents/hephaestus.py` | `begin_session` / `end_session` worktree isolation, `PolicyGate` (`src/anima_core/tools/policy.py`), test feedback loop, `_hephaestus_orchestrator.py` parallel delegation strategy. All of this runs against a repo checkout, not against HTTP. |
| `CostTracker` | `src/anima_core/cost/tracker.py` | Fire-and-forget, agent-agnostic. No server coupling. |
| `TraceRecorder` | `src/anima_core/trace/recorder.py` | Fire-and-forget, agent-agnostic. No server coupling. |
| `CalliopeClient` interface | `src/anima_core/calliope/client.py` | Stable method surface: `create`, `get`, `update`, `batch_create`, `query`, `search`, `traverse`, `lineage`, `impact`, `review`, `update_links`. ArtifactService underneath. Direct MongoDB access anywhere else is a bug to eliminate, not a pattern to carry. |
| All six agent classes | `src/anima_core/agents/` (`hermes.py`, `clio.py`, `hephaestus.py`, `urania.py`, `mnemosyne.py`, `pavel.py`) | The agent logic is server-independent. What carries is the loop + tool surface + Calliope interaction; what dies is the FastAPI wiring that invokes them. |
| Relay trail tools | `src/anima_core/tools/relay.py` — `open_relay`, `append_crossing`, `close_relay`, `abandon_relay`, `write_context_snapshot` | The relay record is the unit of durable session state. This already replaces the server session table for in-flight work. |
| Dispatch tools + pipeline driver | `src/anima_core/tools/dispatch.py` — `plan_with_clio`, `build_with_heph`, `verify_with_urania` | The three-phase pipeline (plan → build → verify) is a domain invariant. `dispatch.py` drives it without any HTTP dependency. |
| `web_fetch` | `src/anima_core/tools/web.py` | Live, implemented over `httpx`. Targeted dependency-doc lookup for Hephaestus. Carries. |
| `spawn_swarm` manifest writer | `src/anima_core/tools/telescoping.py` | The write-manifest step is correct and live. The executor was never built (see Known Gaps). |
| Tree-sitter prepass + SemanticMCPOrchestrator | `src/anima_core/agents/mnemosyne.py`, `src/anima_core/tools/tree_sitter_prepass.py`, `src/anima_core/tools/semantic_mcp_orchestrator.py` | Mnemosyne's structural prepass (tree-sitter language detection + per-file symbol inventory, SemanticMCPOrchestrator for LSP process lifecycle) runs before the first LLM call. This is a concrete dependency, not just an ADR footnote — aZero Mnemosyne must wire both. Governed by `adr-deterministic-structural-context-for-mnemo-033`. |
| `probe_events` + `shitcorpus` tools | `src/anima_core/tools/probe_events.py`, `src/anima_core/tools/shitcorpus.py` | Both are live, wired to agents. `write_probe_event` wired to Hermes and Urania; `write_discard_record` wired to Mnemosyne, Hephaestus, Clio, Hermes. Carry forward with same wiring. |
| `image_to_text` tool | `src/anima_core/tools/vision.py` | Live, implemented via Claude Vision Haiku. Wired to Mnemosyne for Confluence image attachments. Carries. |
| Instance `crypto.py` Fernet pattern | `src/anima_core/instance/crypto.py` | Fernet encrypt/decrypt for credentials is the right primitive. The SQLite ORM layer dies; the cryptographic contract carries (see Carries Reshaped). |
| Six agent capability map artifacts | Calliope — `agent-capability-*` series, all `semi_liquid` | The capability map is the governed record of what each agent can and cannot do. Liquidity is semi_liquid — carries forward as the reference for aZero agent composition. |
| All frozen domain knowledge | Calliope — 116 `frozen` artifacts (corpus spine) | Frozen by definition. Carries forward unchanged into any topology. |
| Live agent prompt artifacts | Calliope — `prompt-hermes-001` chain, `prompt-clio-001`, `prompt-hephaestus-001` chain, `prompt-mnemosyne-001`, `prompt-urania-001`, `prompt-pavel-001` | These are the authoritative prompts. Disk files in `prompts/` are human-readable aliases only (confirmed: `base.py` loads from Calliope, falls back to disk only if Calliope fails). |
| Constellation version 8 | Calliope — `anima-constellation-current-succ-bf7043e1` | The live topology map. aZero's `_ensure_context_loaded` will point at this same artifact ID. |
| Drive script interaction pattern | `scripts/drive_*.py` (multiple) | Multi-turn message accumulation, substantive completion gates, pre-session backup, transcript recording. This is the discovered correct CLI shape. The scripts themselves are superseded; the pattern they embody is the aZero design target. |

---

## Dies with the server model

| Item | Why it dies | Reshapes into |
|------|-------------|---------------|
| `FastAPI` application | `src/anima_core/app.py` + `src/anima_core/web/router.py`. aZero is a library + daemon, not a request-response server. The server model was the correct bootstrap shape; the friction it created (drive scripts, workarounds) revealed the right shape. | aZero daemon surface — direct agent invocation with configurable triggers, no HTTP layer between caller and agent. |
| `AnimaAuthMiddleware` | `src/anima_core/middleware.py`. Verified: non-local topology path returns HTTP 401 with `# TODO: replace with real auth`. It was always a stub — auth was deferred. In a CLI/daemon model, auth lives at the daemon boundary, not inside an HTTP middleware class. | Auth at the daemon boundary. The daemon decides who may invoke it; agents themselves don't authenticate. |
| `_build_artifact` (private function in `web/router.py`) | `src/anima_core/web/router.py:1692`. Proposal commit logic was embedded in the HTTP router rather than extracted as a service. `scripts/drive_mnemosyne_self.py:57` imports it directly with `from anima_core.web.router import _build_artifact` — a confirmed coupling smell. | Mnemosyne proposal commit path becomes a clean service call on `ArtifactService` / `CalliopeClient`. No private import. |
| `src/anima_core/web/router.py` (entire file) | 2000+ line HTTP router — form data parsing, WebSocket session handling, streaming pipeline over WS, static file serving. All of this is the server model. | Agent invocation logic extracted into service layer. WS streaming becomes a stream of events from a daemon socket or stdout, depending on aZero's chosen IPC surface. |
| `src/anima_core/web/polling.py` (`UraniaSweeper`) | Runs as `asyncio.create_task` inside the FastAPI lifespan (`app.py`). Dies when the server process dies. Sweep behavior is correct; lifecycle binding to a server process is not. | See Carries Reshaped. |
| `src/anima_core/web/templates/` | Server-side rendered HTML templates. aZero has no web UI surface. | No direct analog. UI concerns move to anima-viz (Electron, horizon+). |
| `src/anima_core/calliope/router.py` | FastAPI router exposing Calliope CRUD over HTTP. aZero talks to Calliope through `CalliopeClient`, not through a local HTTP proxy. | `CalliopeClient` is the entire interface. The HTTP router layer disappears. |
| `src/anima_core/instance/router.py` + `instance/` SQLite brain (as server concept) | Six-table SQLAlchemy ORM (`users`, `user_preferences`, `sessions`, `instance_config`, `ui_state`, `connector_config`) — server session management, OAuth stubs, HTTP auth gate. None of these are meaningful in a single-user local daemon. | See Carries Reshaped. |
| `src/anima_core/jobs/data_provenance_sweep.py` as server-lifecycle-bound background job | Wired into FastAPI lifespan loop in `app.py`. Same failure mode as UraniaSweeper — dies with the server process. | See Carries Reshaped. |
| `src/anima_core/hephaestus/bridge.py` | Originally a subprocess invocation shim for Claude Code; evolved into a Calliope artifact renderer that starts a `HephaestusAgent`. The docstring confirms the subprocess purpose dissolved: "the bridge no longer spawns an external process." The module boundary is wrong — neighbor expansion + prompt rendering are Hephaestus's concern, not the dispatcher's. | Neighbor expansion + prompt rendering carry into `hephaestus/context.py` (new module). `dispatch.py::build_with_heph` calls it. Dispatch stays a thin coordinator; Hephaestus owns its own context preparation. `bridge.py` module name and its CLI `__main__` entry point die. |
| `src/anima_core/hephaestus/ws_events.py` | WebSocket event forwarding shim. Makes sense only in the context of a WS streaming loop in `web/router.py`. | aZero uses a different event emission surface (daemon socket, stdout events, or a callback). The `make_pipeline_callback` pattern carries as a concept; the WS-specific implementation dies. |
| Hardcoded absolute paths in drive scripts | Multiple `scripts/drive_*.py` files contain hardcoded `/Users/wmorgus/...` paths. | Die with the scripts. aZero resolves paths relative to user config (`~/.azero/`). |
| Raw `MongoClient` direct access | Some drive scripts bypass `ArtifactService` / `CalliopeClient` by opening a direct `MongoClient` connection. | Must NOT pattern-carry. All Calliope access in aZero goes through `CalliopeClient`. Direct Mongo access is a violation of the validation and provenance contract. |

---

## Carries reshaped

These items have correct substance but wrong form. The substance carries; the form changes.

**Instance brain → local config + Calliope relay**

The six SQLite tables held real concerns. They reshape as follows:

| Old table | Substance | aZero form |
|-----------|-----------|------------|
| `connector_config` (credentials_blob) | Encrypted connector credentials | `~/.azero/secrets.toml`, Fernet-encrypted (same `instance/crypto.py` primitive — that file carries) |
| `instance_config` + `user_preferences` | Instance-level and user-level settings | `~/.azero/config.toml` — analogous to Claude Code's `settings.json` |
| `sessions` (session resume, last_will_message, calliope_project_id) | Durable session state and resume capability | Relay artifacts in Calliope (`open_relay` / relay record chain) — already live |
| `users` + auth gate | Author-reviewer identity | Calliope authority model — `provenance()` on every artifact write handles this; no separate user table needed for single-user local daemon |
| `ui_state` | Per-surface UI persistence | Not a daemon concern; moves to anima-viz if needed |

**UraniaSweeper → configurable sweep triggers**

`UraniaSweeper` in `web/polling.py` runs as a FastAPI background task. The behavior (sweep Calliope for unprocessed `pull_request` and `deployment_record` artifacts, invoke Urania) is correct. The server-lifecycle binding is not.

aZero should expose configurable sweep trigger modes:
- `on_load` — sweep once at daemon start
- `on_cron` — interval-based (replaces the `interval=60` default)
- `on_pr` — triggered when a `pull_request` artifact is written
- `on_artifact` — triggered on any new pending artifact of a configurable type

Same `UraniAgent` invocation underneath; only the trigger surface changes. **This is a design direction, not a settled decision** — it is flagged here so the aZero build can wire it correctly rather than re-creating a server-lifecycle binding by default.

**Data provenance sweep → scheduled invocation or configurable trigger**

`jobs/data_provenance_sweep.py` + the lifespan loop in `app.py`. Same failure mode as UraniaSweeper. In aZero: either a standalone scheduled invocation (cron job, launchd plist) or part of the configurable sweep trigger system above. The Snowflake adapter and `run_drift_sweep` logic carry; the lifespan binding dies.

---

## Known gaps (carry as-is)

These are not regressions — they were known gaps before aZero. They carry as acknowledged open surfaces, not inherited solutions.

| Gap | Evidence | aZero disposition |
|-----|----------|-------------------|
| `spawn_swarm` executor never built | `src/anima_core/tools/telescoping.py` writes a `swarm_manifest` artifact with `status='open'` and returns the manifest ID. No parallel process launch, no child agent invocation, no result aggregation. File docstring confirms this explicitly. | aZero should implement the executor. The manifest-writing step is correct; the execution layer is the missing half. |
| `web_search` returns `[]` always | `src/anima_core/tools/web.py` — `_search_backend` is `None`. No sprint contract ever wired a backend. Returns `[]` on every call by design ("contract-correct empty result"). `web_fetch` is fully live. | aZero either wires a real backend (Anthropic server-side web_search, Tavily, or Brave — the TODO in `web.py` lists the options) or drops `web_search` from the tool surface entirely. It should not appear as a live capability without a backend. |
| Pavel §6.14 corpus envelope is OPEN | `PavelAgent` (`src/anima_core/agents/pavel.py`) carries forward, but the §6.14 corpus governing Pavel's scope is not ratified. The corpus surface is ungoverned. | PavelAgent is included in aZero but must be flagged as ungoverned until §6.14 ratification. Do not treat Pavel's behavior as spec-stable. |
| Calliope graph retrieval is flat/lexical | All retrieval in `src/anima_core/calliope/` is flat query + lexical search. Graph edges (`relates_to`, `supersedes`, `parent_artifact_id`) exist in the schema (Tier-1 CAL-02/03 live) but structural traversal is never used in retrieval paths. | Carry as known gap. The chunking + semantic retrieval sprint (self-directed backlog item #1) is the paired fix. Both halves only pay off together. |
| Telescoping executor + chunking+retrieval deferred | Both are self-directed backlog items confirmed deferred. | Run through Anima, not by hand. Not pre-conditions for aZero's initial build. |

---

## Stale references

References that exist in the codebase or Calliope artifacts that are no longer accurate. Future work must not treat these as live constraints.

| Stale reference | What it says | What is actually true |
|----------------|--------------|----------------------|
| `dec-019`, `dec-020` | ADRs referencing a Will→Iris invocation chain (Will agent hands off to Iris agent hands off to specialist). | Hermes absorbed Will + Iris on May 25, 2026 (Phase 12). `HermesAgent` (`src/anima_core/agents/hermes.py`, `agent_name = "Hermes"`) is the consolidated front door. The Will/Iris agent classes do not exist in the codebase. |
| `adr-synchronous-agent-invocation-v2` | Describes Will→Iris→specialist as the canonical invocation chain. | Stale. Current pattern: Hermes→specialist via `tools/dispatch.py` (`plan_with_clio`, `build_with_heph`, `verify_with_urania`). |
| Any ADR/artifact referencing `IrisAgent`, `WillAgent`, `iris.py`, `will.py` as separate agent files | These files do not exist. The agents do not exist. | Hermes is the single front door. These references are archaeology from pre-Phase-12. |
| Pavel `§6.14` corpus references (if marked ratified anywhere) | May appear in notes or drafts as if ratified. | Confirmed OPEN as of 2026-06-16. Not ratified. |
| `adr-hephaestus-two-phase-execution` | Referenced in `bridge.py` docstring as "historical context pending formal deprecation work (queue item 010)." | Stale. Direct HephaestusAgent execution replaced the two-phase subprocess model. The ADR describes a design that no longer exists. Queue item 010 to formally deprecate it remains open. |
| `UraniAgent` class name (missing 'a') | `src/anima_core/agents/urania.py:22` — class is `UraniAgent`, not `UraniaAgent`. All import sites use `UraniAgent`. | aZero should rename to `UraniaAgent` at the class level. Cosmetic defect — no behavior change. |

---

## Load-bearing decisions for the aZero build

Decisions that directly constrain aZero design. Violating these is not a design choice — it is a governance defect.

### Frozen (immutable)

| Artifact ID | Constraint |
|-------------|------------|
| `dec-021` | Sub-agent spawning model — governs which agents may spawn sub-agents and under what conditions. Telescoping license list (Mnemosyne, Clio, Urania) derives from this. |

### Semi-liquid (stable, may evolve through governed process)

| Artifact ID | Constraint |
|-------------|------------|
| `adr-hephaestus-direct-execution` | HephaestusAgent executes directly — no subprocess, no Claude Code invocation. `bridge.py`'s current behavior is already aligned with this; the module boundary is the only thing dying. |
| `adr-relay-record-unit-hermes-writer-001` | Relay record is the unit of durable session state. Hermes is the writer. aZero's session persistence model flows from this. |
| `adr-hermes-agent-dispatch-051-001` | Hermes dispatches to specialists via the three dispatch tools (`plan_with_clio`, `build_with_heph`, `verify_with_urania`). This is the canonical invocation pattern — not direct agent construction in user code. |
| `adr-agent-context-one-hop-cites-001` | Each agent's runtime context is one-hop Calliope cites from the constellation entry. No disk reads for context. Disk files are human-readable aliases only. `_ensure_context_loaded` in `base.py` implements this. |
| `adr-deterministic-structural-context-for-mnemo-033` | Mnemosyne's context loading is deterministic and structural — not semantic search. Constrains how Mnemosyne's constellation entry is populated and how its cites list is maintained. |
| `calliope-ad-caller-assigned-ids` | Artifact IDs are assigned by the caller (agent), not generated server-side. All `create` calls in aZero must carry a deterministic ID from the creating agent. |
| `calliope-ad-bfs-not-graphlookup` | Graph traversal uses BFS in application code, not MongoDB `$graphLookup`. Performance and correctness rationale is in this ADR. Do not replace with `$graphLookup`. |

### Active audit chain constraint

The live pipeline audit chain is: `sprint_contract → build_decision → pull_request → build_verification`.

`execution_prompt` is deprecated — no new `execution_prompt` artifacts should be written in aZero. `bridge.py` already removed the `_save_execution_prompt` call (confirmed in code). The deprecation is formal in `dec-021`-series context; the implementation is clean.

### Calliope Tier-1 pure-append semantics

`CAL-02` / `CAL-03` are live (confirmed Jun 10, 2026). `parent_artifact_id` + `supersedes` chain is in the live schema. aZero must write supersession records when updating frozen or semi-liquid artifacts — never in-place mutation.
