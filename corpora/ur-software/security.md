# Ur-Software Corpus — Security

Frozen reference for security reasoning. Argus reasons FROM this, not about it. Updates are supersession events, not edits. Open surface marked [OPEN].

Three tiers:
- **Frozen**: invariants that have not moved in decades. Epistemic tag required: [theorem] (mathematically proven), [empirical] (well-observed, defeasible by counterevidence), [axiom] (staked-not-proven foundational commitment), [definition] (formal definition with provable properties).
- **Semi-liquid**: pattern wisdom with because. Fields: *because*, *canonical failure* (mechanistic — the causal path, not the symptom), *signals* (observable conditions suggesting this pattern applies), *cross-refs*.
- **Liquid**: external retrieval targets. NOT static knowledge — the agent queries this tier at decision time, does not memorize it. Argus has web search + advisory-database lookup tools scoped to this tier. Naming retrieval targets is the contract; their contents are out of scope for this document and change faster than the document can.

Relationship to other corpora: security is cross-cutting. Trust boundaries are application concerns made adversarial; TOCTOU is a concurrency invariant with security consequences; transport security answers the "network is secure" distributed fallacy; encryption-at-rest and key management are least-privilege questions in the data domain. [→ corpus_ursoftware_application] [→ corpus_ursoftware_concurrency] [→ corpus_ursoftware_distributed] [→ corpus_ursoftware_data]

---

## §1 Frozen invariants

1.1 Kerckhoffs's principle `[axiom]` — A cryptographic system must remain secure when everything about it except the key is public knowledge. Security derives from key secrecy, not mechanism secrecy. Rules out: security through obscurity as a primary control; custom protocols whose safety depends on attackers not knowing the design; treating source-code closure as a security property.

1.2 CIA triad `[definition]` — Three distinct security properties with distinct failure modes and distinct attacker goals. Confidentiality: unauthorized parties cannot read. Integrity: unauthorized parties cannot modify (or modification is detectable). Availability: authorized parties can access when needed. The three are not reducible to each other; a control that improves one may degrade another. Rules out: treating "security" as a single scalar; using a confidentiality control (e.g., encryption-at-rest) as evidence of integrity; conflating DDoS mitigation with authentication hardening.

1.3 Authentication vs. authorization `[definition]` — Authentication establishes *who* (identity claim, verified). Authorization establishes *what that identity is permitted to do* (policy decision against identity + resource + action). They are distinct operations performed at distinct points with distinct failure modes. Rules out: assuming a valid authentication implies authorization for a given action; treating a session token as proof of permission rather than proof of identity; auth checks at the edge that are not re-evaluated when context changes.

1.4 Least privilege `[axiom]` — Every component (user, process, service, credential) operates with the minimum permissions required for its function, and only for the duration required. Rules out: broad permission grants "for convenience" or "we'll tighten later"; shared credentials across services; ambient authority where any code in a process inherits the process's full permissions; long-lived credentials where short-lived ones are feasible. [→ corpus_ursoftware_data — encryption-at-rest and key management are least-privilege questions; who has access to the key is as important as how the key is stored]

1.5 Defense in depth `[axiom]` — No single control is assumed to hold. Controls layer such that breach of one does not compromise the whole. Each layer is designed under the assumption that outer layers have already failed. Rules out: single-point security decisions; "we have a WAF" / "we have a firewall" as a complete posture; trusting input because it passed a prior layer's check.

1.6 Trust boundary `[definition]` — A point at which data or control crosses from a less-trusted context to a more-trusted one. Every input crossing such a boundary is attacker-controlled with respect to the more-trusted side and must be validated, authenticated, or both at the crossing. The boundary is a property of the data flow, not of the network topology. Rules out: trusting client-supplied data on the server because "our client sends it correctly"; assuming internal network requests are safe; trusting environment variables, filenames, or deserialized objects without validation; locating trust at the firewall instead of at the data flow. [→ corpus_ursoftware_application §1.3 — ports and adapters are the architectural expression of trust boundaries]

1.7 Complete mediation `[axiom]` — Every access to every object must be checked against the access control policy on every request. No cached permission, no assumed-from-prior-check authority. Rules out: caching authorization decisions across requests without a cache-invalidation strategy tied to policy changes; "we checked on login" as a substitute for per-request checks; assuming a prior successful access implies continuing permission. (Saltzer & Schroeder, 1975. Distinct from trust boundary: trust boundary tells the agent *where* to check; complete mediation tells it *always*.)

1.8 Confused deputy `[theorem]` — A component holding more authority than its caller can be induced by the caller to exercise that authority on the caller's behalf. The deputy acts within its permissions on instructions whose origin it has failed to authenticate. Rules out: ambient authority in APIs (authority attached to the process, not to a capability passed with the request); treating CSRF, SQL injection, SSRF, and LLM prompt injection as unrelated bug classes — they are instances of the same theorem at different deputy boundaries. (LLM prompt injection: the model with tool access is the deputy; untrusted text the model reads is the attacker-controlled instruction. The theorem fits exactly.)

1.9 Timing side channel `[theorem]` — Any operation whose execution time is a function of secret data leaks information about that data to any observer who can measure timing. The leak is mathematical, not implementation-dependent; "the difference is too small to exploit" is a measurement claim that has been refuted across LAN, WAN, and cross-VM boundaries. Constant-time comparison is the only correct mitigation for secret comparison. Rules out: early-exit string comparison on secrets, MACs, tokens, or password hashes; "network jitter masks it" reasoning; treating timing as a non-channel. [→ corpus_ursoftware_concurrency §1.8 — cache-line timing is the same mechanism at finer granularity]

1.10 Don't roll your own cryptography `[axiom]` — Cryptographic primitives require properties (constant-time execution, side-channel resistance, correct parameter selection, formally analyzed mathematical foundations) not achievable by general-purpose implementation without specialist expertise and adversarial review. Two distinct failure paths: (1) implementing a primitive from scratch; (2) using a vetted primitive incorrectly — AES in ECB mode, nonce reuse in AES-GCM, ECDSA with a static or reused nonce. Both paths produce broken cryptography; the second is more common against teams that know not to do the first. Rules out: implementing AES, RSA, ECDSA, or hash functions from scratch; custom KDFs; "encryption" via XOR or rotation; novel protocol composition without formal analysis; AES-ECB for anything; GCM without guaranteed nonce uniqueness.

1.11 Cryptographic agility / algorithm lifecycle `[empirical]` — Every cryptographic algorithm has a finite lifetime. Algorithms move from recommended → deprecated → broken as cryptanalysis and compute advance. A system that hardcodes a primitive cannot migrate when the primitive falls. Rules out: hardcoding algorithm choices at call sites; storage formats that do not record the algorithm and parameters used; assuming "AES-256 is fine forever"; treating the post-quantum transition as a future problem. (Empirical, not theorem — defeasible by the appearance of a primitive that doesn't age, but no such primitive has been observed in the history of the field.)

1.12 Allowlist over denylist `[axiom]` — Input validation must define what is permitted (allowlist) rather than what is forbidden (denylist). Denylist thinking is structurally wrong: the attacker's input space is infinite and cannot be enumerated; every denylist is a partial enumeration of known-bad that leaves unknown-bad unblocked. Rules out: filtering input by removing "dangerous characters"; building injection defenses on character blacklists; "we strip semicolons and single quotes" as a parameterization substitute; any validation logic whose correctness depends on completeness of a forbidden-pattern list.

---

## §2 Semi-liquid patterns

### Injection prevention via parameterization
*because:* Injection (SQL, command, LDAP, XPath, template, NoSQL) is a single bug class: attacker-controlled data is interpolated into a string subsequently parsed as code in a more-privileged context. Parameterized queries, prepared statements, and argument-array APIs separate code from data at the interface, structurally denying the attacker access to the parser.
*canonical failure:* Developer reaches for string concatenation on the "simple" or "internal" query where parameterization "isn't worth it." The attacker-controlled value closes the quoted literal, appends a statement terminator, and adds a second statement the parser executes under the deputy's privileges. The seam exists at every site where user input touches a query, not only at obvious "search" fields.
*signals:* String-building of queries, shell commands, or templates from variables anywhere in the codebase; ORM "raw" or "execute" escape hatches in code review; reports of unusual characters (apostrophes, semicolons) breaking functionality — these surface the parsing seam an attacker would probe.
*cross-refs:* [→ §1.6 trust boundary — the parser is on the trusted side of the boundary] [→ §1.8 confused deputy — the database or shell is the deputy] [→ §1.12 allowlist — parameterization is the structural implementation of allowlist thinking at the query boundary]

### Context-aware output encoding
*because:* The same byte sequence has different meanings in different output contexts (HTML body, HTML attribute, JavaScript string, URL parameter, CSS value). Encoding must be applied at the point data enters the target context, using the encoding correct for *that* context — not for the context it came from.
*canonical failure:* Encoding applied at input time ("sanitize on write"). Data stored "clean" against an assumed output context is later retrieved into a different context — an HTML-escaped string interpolated into a JavaScript literal — where the original encoding was wrong. Stored XSS survives because the persistence layer guessed wrong about the eventual consumer.
*signals:* Sanitization at the model or persistence layer rather than the view layer; multiple output surfaces (web, email, mobile, API) reading the same stored field; template auto-escaping disabled "for this one partial."
*cross-refs:* [→ corpus_ursoftware_application §1.3 — encoding belongs at the adapter (output port), not the domain]

### Authentication hardening
*because:* Authentication endpoints are the highest-value targets and the most-probed surface. Fast hash functions (SHA family, MD5) are designed for throughput; password hashing requires slowness and tunable cost. Rate limiting, lockout, and MFA convert offline-economic brute-force into online-economic attacks where each guess costs a network round-trip.
*canonical failure:* Rate limit applied to `/login` but not to adjacent endpoints exercising the same credential check: `/api/login`, `/password-reset`, `/oauth/token`, account-existence oracle in signup or forgot-password flows. The control was placed at a URL, not at the authentication operation. Attacker pivots to the unprotected sibling.
*signals:* Multiple endpoints touching the password verifier or user-existence oracle; rate-limit middleware applied by route prefix rather than by operation type; password hashes stored with SHA-family or unsalted constructions; no documented credential-stuffing posture.
*cross-refs:* [→ §1.3 authentication vs. authorization] [→ §1.9 timing side channel — password comparison must be constant-time] [→ §1.7 complete mediation — rate limiting is per-operation, not per-endpoint]

### Secret management
*because:* Secrets in source, in images, or in long-lived environment variables conflate the secret's lifetime with the artifact's lifetime. Vault-issued, short-lived, runtime-injected secrets bound blast radius and make rotation a normal operation rather than an incident.
*canonical failure:* Secret rotated in the vault; the process loaded its value into memory at startup and holds a stale copy. Rotation has no effect until restart. Only some replicas restart, producing a split: part of the fleet authenticates with old credentials, part with new. The rotation appears successful while half-failed; the old credential remains valid.
*signals:* Secrets read once at boot and held in process state; rotation procedures with no documented restart or refresh step; secrets in `.env` files committed to source or shared via chat; `git log -p` containing credentials.
*cross-refs:* [→ §1.4 least privilege — short-lived, narrowly scoped credentials are the operational expression of least privilege]

### CSRF protection at the operation, not the endpoint
*because:* State-mutating operations must verify that the request was intentionally issued by the authenticated user, not induced by a third-party origin exploiting ambient cookie authority. The check belongs on the operation, not on a specific route.
*canonical failure:* CSRF token validated on the HTML form-submission handler but not on the JSON API endpoint performing the same state change. The team protected "the form" rather than "the operation." Attacker invokes the JSON endpoint cross-origin; no token check fires; the operation succeeds.
*signals:* CSRF middleware scoped by content-type or route prefix; "API endpoints don't need CSRF, they use tokens" reasoning unaccompanied by audit of which tokens carry origin-binding; cookie-based session auth used by both HTML and JSON surfaces simultaneously.
*cross-refs:* [→ §1.8 confused deputy — CSRF is the canonical browser-as-deputy attack] [→ §1.7 complete mediation — the check must fire on every state-mutating request, not every state-mutating route]

### Transport security everywhere
*because:* Plaintext on any segment is readable and modifiable by any party with access to that segment. "Internal network" is a topology claim, not a trust claim. TLS everywhere, certificate validation, HSTS, and mutual TLS where appropriate make transport-layer compromise an attack on the certificate authority rather than an attack on the wire.
*canonical failure:* Service-to-service traffic on plain HTTP "inside the cluster" because TLS is "handled at the edge." A compromised internal host, misconfigured service mesh, or lateral-movement foothold reads or modifies traffic the architecture assumed was unobservable. The perimeter model was load-bearing and broke silently when the interior was reached.
*signals:* Mixed TLS / plaintext within a deployment; certificate validation disabled in clients ("for dev," never removed); HSTS absent on user-facing origins; internal services exempt from the TLS policy applied to edge traffic.
*cross-refs:* [→ corpus_ursoftware_distributed §1.3 — "the network is secure" is the eighth fallacy of distributed computing]

### Dependency vulnerability management
*because:* Most production code is dependency code. CVEs accrue against specific versions; exposure is determined by what is locked, not what is latest. Automated scanning closes the gap between disclosure and awareness; lock files make the dependency inventory authoritative.
*canonical failure:* Dependency updated to patch a CVE; changelog not read; the patch release changed a default (cookie SameSite behavior, TLS version floor, deserializer trust policy) such that a previously safe call site is now unsafe. The vulnerability was patched and a new one was introduced in the same operation.
*signals:* No lock file, or lock file not enforced in CI; CVE scanner present but advisories not triaged; "we update when something breaks"; transitive dependencies invisible to the team's inventory; pinned to exact versions with no automated update process — this freezes the exposure profile without closing it; the team stops drifting into new vulnerabilities but also stops moving away from known ones.
*cross-refs:* [→ §4 liquid tier — this pattern is the operational consumer of the NVD and GHAD retrieval targets]

### Session lifecycle
*because:* Sessions that persist beyond their useful scope accumulate risk: credentials can be stolen and replayed, privileges can outlive their grant, and session state can be fixed before authentication and then elevated after. Correct session management bounds exposure at each transition.
*canonical failure:* Session fixation — attacker obtains a pre-authentication session token (via URL parameter, predictable cookie value, or shared link), victim authenticates, server promotes the existing session to authenticated status without issuing a new token. The attacker's known token is now authenticated. The rotation step (issue new session ID on privilege change) was the missing control; expiry was irrelevant.
*signals:* Session ID not rotated on login, logout, or privilege-level change; session tokens with no absolute timeout, only idle timeout; "remember me" tokens with the same privilege scope as interactive sessions; session invalidation on logout that clears the client cookie without invalidating the server-side record.
*cross-refs:* [→ §1.3 authentication vs. authorization — session rotation belongs at every authentication event, not just initial login] [→ §1.7 complete mediation — server-side invalidation is required; client-side cookie deletion alone is insufficient]

---

## §3 Supersession spine

Security posture has evolved through paradigms. Each step shows Aufhebung: the prior model's failure mode is preserved as historical evidence, negated as the sole answer, and elevated — its valid insight retained — in the successor. Newer is not better in isolation; context determines which posture fits.

**Perimeter model** — strong outer boundary, trusted interior. *Insight retained:* network segmentation has real value; not all traffic should reach all services. *Negated by:* insider threat, lateral movement after initial breach, the dissolution of "interior" under cloud / SaaS / remote work. The interior was never trustworthy; the perimeter model made that assumption invisible until it failed.

**Defense in depth** — layered controls, no single point of failure. *Insight retained:* §1.5; this remains a frozen axiom. The layering principle is correct and survives. *Negated as sole answer by:* supply chain attacks (SolarWinds, xz-utils, event-stream) where the attacker enters through a trusted layer that all other layers were configured to pass. Controls were independent against external adversaries and correlated against supply-chain adversaries — the attack entered through the trust, not around it.

**Zero trust** — identity-verified, per-request authorization, no implicit trust from network location. *Insight retained:* trust attaches to verifiable claims about principals and actions, not to network topology. §1.7 (complete mediation) is the formal expression of this. *Currently stress-tested by:* AI-assisted credential attacks at scale; LLM prompt injection as a new confused-deputy vector (§1.8) where the model-with-tools is the deputy and untrusted text is the instruction; deepfake-assisted social engineering against the identity-verification steps zero trust depends on.

**Verifiable software supply chain** (emerging, unsettled) — cryptographic attestation of build provenance (SLSA, sigstore, reproducible builds); software bill of materials (SBOM) as a first-class artifact; signed releases with auditable build pipelines. *Insight being elevated:* defense in depth failed against supply-chain entry because the trust granted to dependencies was unverified and invisible. The successor makes provenance verifiable and the dependency graph auditable. Not yet a settled posture — the field is building the tooling and the norms simultaneously. Argus treats this as the emerging current step; its specific instantiations are liquid-tier knowledge, not frozen.

---

## §4 Liquid tier — retrieval targets

This tier is architecturally distinct from the liquid tiers of the other ur-software corpora. In those corpora, liquid means "the agent generates specifics from context." Here, liquid means "the agent looks specifics up from authoritative external sources at decision time." Enumerating vulnerabilities, advisories, algorithm recommendations, or framework-specific guidance statically in this document would be wrong: the document cannot be re-issued at the cadence this information changes, and stale security knowledge is worse than absent security knowledge because it is trusted.

Argus is provisioned with retrieval tooling scoped to this tier. The contract this corpus makes is to name the retrieval targets and specify retrieval discipline. Their contents are out of scope.

**Named retrieval targets:**
- **NIST National Vulnerability Database (NVD)** — CVE lookup by dependency name and version; CVSS scoring; CWE classification. Primary source for "is this version vulnerable."
- **GitHub Advisory Database (GHAD)** — ecosystem-scoped advisories (npm, PyPI, Maven, RubyGems, Go, NuGet, Composer, Rust). Often surfaces ecosystem advisories before NVD assigns a CVE.
- **OWASP Top 10 (current edition)** — periodic synthesis of prevalent web application vulnerability classes. The edition matters; the corpus does not hardcode the list — Argus retrieves the current edition.
- **NIST cryptographic algorithm recommendations** — current guidance on approved algorithms, key sizes, deprecation timelines, and the post-quantum transition. Authoritative source for §1.11 decisions.
- **Vendor / framework security advisories** — Django, FastAPI, SQLAlchemy, Rails, Spring, Node.js, etc. Framework-specific defaults and known-bad configurations are versioned with the framework.
- **CISA Known Exploited Vulnerabilities (KEV) catalog** — CVEs with confirmed in-the-wild exploitation. Prioritization signal: a KEV-listed CVE warrants a different response posture than an equally-scored non-KEV CVE, regardless of CVSS score.

**Retrieval discipline:**
- Argus cites the retrieval source and timestamp for any claim sourced from this tier. A liquid-tier claim without a citation is not yet evidence.
- Argus distinguishes "no advisory found at retrieval time" from "no advisory exists" — the former is bounded by the freshness of the source and the precision of the query.
- When retrieval is unavailable, Argus declares the gap rather than substituting frozen-tier reasoning for a liquid-tier question. Frozen invariants do not answer "is this specific version of this specific library safe" — that is a retrieval question.

---

## Security

This IS the security corpus. Agents in the Anima constellation route security-relevant decisions to Argus. Argus reasons from the frozen and semi-liquid tiers of this document and from live retrieval at the liquid tier. Decisions that depend on liquid-tier information made without retrieval are declared as such and escalated for human review.
