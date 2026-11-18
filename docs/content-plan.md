# GovernedRuntime Content Plan
**File:** /docs/content-plan.md
**Description:** Source of truth for the 24-post series: build order, platforms, teasers, code modules and status.
**Author:** Libor Ballaty
**Created:** 2026-11-18

Status: Draft. Series start date is not set, so weeks are relative (W1 to W12, two posts per week).

## How the series works

The series builds one system, in the order an implementer would have to think about it. Each post solves
one problem on the way, and the system can do something new after every post. A post depends only on
posts before it.

Three tracks run in parallel for every post:

| Track | What | When |
|---|---|---|
| Teasers | One LinkedIn post and one Substack Note pointing to the article | Before the article |
| Article | The full piece, on Substack or as a LinkedIn article | Publication day |
| Code | The module in this repo that implements the concept, tagged `post-NN` | Merged and tagged before the article |

Totals: 24 articles (12 Substack, 12 LinkedIn), 48 teasers, 24 code deliverables. There is no short-post
format. Each week pairs one Substack piece with one LinkedIn article.

## Month 1: Contain and identify (W1 to W4)

| # | Wk | Title | Platform | Code | Status |
|---|---|---|---|---|---|
| 1 | 1 | Stop Treating AI Agents Like Team Members. Treat Them Like Unvetted Microservices | Substack | `modules/01_sandbox/sandbox_runner.py`, `modules/01_sandbox/strict_agent.sbpl` | planned |
| 2 | 1 | API-Driven vs Subscription-Driven Agents: Why the Threat Model Changes | LinkedIn article | `modules/01_sandbox/session_classifier.py` | planned |
| 3 | 2 | Local-First Economics of AI Inference vs Cloud Token Bloat | Substack | `modules/01_sandbox/cost_benchmark.py` | planned |
| 4 | 2 | Isolating Local SLMs: Ollama and MLX Behind Hard OS Boundaries | LinkedIn article | `modules/01_sandbox/local_slm_cage.sh` | planned |
| 5 | 3 | Ephemeral Capability Leases: Securing Non-Human Identities in Agentic Workflows | Substack | `modules/01_sandbox/token_broker.py` | planned |
| 6 | 3 | Revoking Access Instantly: Dynamic Capability Lease Invalidation | LinkedIn article | `modules/01_sandbox/lease_revoker.py` | planned |
| 7 | 4 | Foundation Review: Assembling the Baseline | LinkedIn article | `daemon.py` (tag `phase-1`) | planned |
| 8 | 4 | Intercepting JSON-RPC: An Inline Authorization Proxy for MCP | Substack | `modules/02_gateway/mcp_proxy.py` | planned |

| # | Problem solved on the way | What the system can do after this post |
|---|---|---|
| 1 | An agent process inherits the full permissions of the user or daemon that runs it. | Agent code runs inside an OS boundary: no outbound network, one writable workspace. |
| 2 | A headless API daemon and a desktop subscription app need different starting boundaries, and nothing tells them apart. | Each session is classified at launch and given a matching initial privilege profile. |
| 3 | There is no measured basis for deciding which workloads run on local models and which go to cloud APIs. | A repeatable benchmark gives throughput, latency and cost per tier to drive placement decisions. |
| 4 | Local inference servers listen on open ports and can read the developer's files and credentials. | Local model servers bind to loopback only and run confined to their model directories. |
| 5 | Agents hold static long-lived tokens, so one compromised session exposes everything the token can reach. | Tools accept only short-lived, scope-bound leases minted by a broker that runs outside the sandbox. |
| 6 | A misbehaving agent keeps its access until its lease expires. | Any active lease can be invalidated immediately across running agent processes. |
| 7 | Sandbox, classifier, broker and revoker are separate tools with no single start-up path. | One daemon starts a classified, sandboxed session with leased credentials. |
| 8 | MCP clients talk straight to tool servers, so no tool call is inspected or authorized. | Every JSON-RPC tool call passes through an inline proxy that checks a lease and records the call. |

## Month 2: Gateway and policy (W5 to W8)

| # | Wk | Title | Platform | Code | Status |
|---|---|---|---|---|---|
| 9 | 5 | The Walled Garden: Governing Subscription-Driven Desktop Harnesses | LinkedIn article | `modules/02_gateway/mcp_config_interceptor.py` | planned |
| 10 | 5 | Defending Against Tool Poisoning and Metadata TOCTOU | Substack | `modules/02_gateway/schema_validator.py` | planned |
| 11 | 6 | Cryptographic Schema Pinning: Stopping Upstream Description Drift in MCP | Substack | `modules/02_gateway/schema_pinning.py` | planned |
| 12 | 6 | Model-Agnostic Fleet Routing Across Heterogeneous LLMs | LinkedIn article | `modules/02_gateway/fleet_router.py` | planned |
| 13 | 7 | Policy-as-Code in Agentic Data Loops | Substack | `modules/03_compliance/policy_evaluator.py` | planned |
| 14 | 7 | The 3-Tier Action Matrix: Structuring Human-in-the-Loop Gating | LinkedIn article | `modules/03_compliance/action_matrix.py` | planned |
| 15 | 8 | State Corruption and Cascading Failures in Multi-Agent Swarms | Substack | `modules/02_gateway/circuit_breaker.py` | planned |
| 16 | 8 | Gateway Review: Hooking the Proxy to the Sandbox | LinkedIn article | `daemon.py` (tag `phase-2`) | planned |

| # | Problem solved on the way | What the system can do after this post |
|---|---|---|
| 9 | Closed desktop clients launch tool servers from their own config files, bypassing the proxy. | Client configs are rewritten, with backup, so configured servers launch through the proxy. |
| 10 | A tool's description or schema can change after approval and carry injected instructions. | The proxy records each tool schema at approval and rejects any call whose schema has changed since. |
| 11 | An in-memory baseline is lost on restart and silently accepts upstream updates. | A persistent hash manifest of tool definitions is verified at startup. Changes need explicit re-approval. |
| 12 | Each model provider has its own tool-call format, so every control would be rebuilt per provider. | Tool calls from any provider are normalized to one set of governance scopes before lease checks. |
| 13 | A valid lease says who may call a tool. It says nothing about which arguments are acceptable. | Each tool call's parameters are evaluated against declarative rules before dispatch. |
| 14 | Every action is treated alike: approve everything (fatigue) or approve nothing (unmonitored autonomy). | Each action routes to one of three tiers: run, run and audit asynchronously, or wait for a human. |
| 15 | One agent's error loop or bad state propagates to the agents that depend on it. | Agents that exceed failure thresholds are tripped and quarantined before the damage spreads. |
| 16 | The gateway components are not wired to the foundation layer. | One daemon runs sandbox, leases, proxy, policy and breakers as a single pipeline. |

## Month 3: Evidence and scale (W9 to W12)

| # | Wk | Title | Platform | Code | Status |
|---|---|---|---|---|---|
| 17 | 9 | Immutable Audit Ledgers: EU AI Act Traceability in Code | Substack | `modules/03_compliance/audit_sink.py` | planned |
| 18 | 9 | Debugging Autonomous Loops: Tracing State Transitions Across Fleets | LinkedIn article | `modules/03_compliance/tracer.py` | planned |
| 19 | 10 | The Compliance Illusion: Why Policy Checkboxes Fail Under the EU AI Act | LinkedIn article | `modules/03_compliance/policy_mapper.py` | planned |
| 20 | 10 | Non-Human Audit Trails: Proving Compliance to External Auditors | Substack | `modules/03_compliance/auditor_report_gen.py` | planned |
| 21 | 11 | Governance for Multi-Tenant AI Backends | Substack | `modules/03_compliance/tenant_isolation_check.sql` | planned |
| 22 | 11 | Performance Overhead vs Security: Benchmarking the Gateway | LinkedIn article | `modules/03_compliance/benchmark_suite.py` | planned |
| 23 | 12 | The State of Enterprise AI: What Actually Works in Production | LinkedIn article | `examples/production_manifest.yaml` | planned |
| 24 | 12 | GovernedRuntime v1.0: End-to-End Orchestration | Substack | `daemon.py` (tag `v1.0`) | planned |

| # | Problem solved on the way | What the system can do after this post |
|---|---|---|
| 17 | Ordinary logs can be edited and lack the decision context an auditor needs. | Every decision is appended to a hash-chained ledger with lease ID, schema version and policy result. |
| 18 | A multi-step, multi-agent run cannot be reconstructed from per-component logs. | Each run carries a correlation ID and an ordered trace of state transitions across nodes. |
| 19 | Runtime evidence exists but is not connected to the regulatory clauses it supports. | Each runtime assertion maps to clause identifiers (EU AI Act, ISO/IEC 42001) for reporting. |
| 20 | Auditors cannot work from raw ledger events. | Compliance summaries are generated from the ledger, with every claim traceable to events. |
| 21 | In a multi-tenant backend, agent queries can cross customer boundaries. | Row-level security policies and verification scripts demonstrate tenant isolation for data and vector stores. |
| 22 | The latency cost of the control stack is unknown, so teams assume it is unacceptable. | Overhead is measured per control (proxy, lease, schema, policy) under load. |
| 23 | There is no single declarative description of a full deployment. | One manifest configures every module for a deployment. |
| 24 | The components lack a unified boot, lifecycle and shutdown path. | One daemon boots, secures and audits the whole stack. |

## Numbering history

Posts were renumbered on 2026-11-18 from the first draft into build order. Nothing had been tagged or
published under the old numbers.

| New | Old | New | Old | New | Old | New | Old |
|---|---|---|---|---|---|---|---|
| 1 | 1 | 7 | 8 | 13 | 14 | 19 | 4 |
| 2 | 3 | 8 | 10 | 14 | 17 | 20 | 21 |
| 3 | 7 | 9 | 9 | 15 | 15 | 21 | 19 |
| 4 | 5 | 10 | 12 | 16 | 16 | 22 | 22 |
| 5 | 2 | 11 | 13 | 17 | 18 | 23 | 23 |
| 6 | 6 | 12 | 11 | 18 | 20 | 24 | 24 |

Two titles changed with the reorder: post 7 was "Month 1 Architecture Review: Assembling the Foundation"
and post 16 was "Month 2 Gateway Review: Hooking the Proxy to the Sandbox".

## Open design flags (settle before the posts they affect)

| Post | Flag |
|---|---|
| 1, 4 | Seatbelt denies operations, it does not strip syscalls. `sandbox-exec` is deprecated by Apple. macOS-only, so a Linux equivalent (bubblewrap, Landlock or seccomp) would widen the audience. |
| 2 | A process can classify a session by launch path and parent process. It cannot reliably identify a closed desktop app. State the limit. |
| 3, 22 | Numbers come from measured runs with hardware and method stated. Cost figures cite a pricing source and date. |
| 5, 6 | The HMAC signing key must be unreadable from inside the sandbox. The broker runs as a separate process. |
| 8 | Proxy port is not chosen. |
| 8 to 16 | The full audit ledger arrives at post 17, but the proxy must record calls from post 8. Decide whether a minimal audit sink ships early. |
| 9 | Rewriting `mcp.json` governs only servers launched from that file, not a client's built-in tools. State the boundary. |
| 10, 11 | Post 10 is the attack and call-time validation against an in-session baseline. Post 11 is the persistent pinned manifest. |
| 19 | Verify the EU AI Act clause mapping against the text. Articles 12, 14 and 19 (logging, human oversight, record-keeping) are likely more relevant than 5 and 50. |
| 21 | SQL and Postgres specific. Needs a test method. |
| 7, 16, 24 | `daemon.py` evolves. Tag each phase so each article links to a stable snapshot. |

## Open decisions

- Series start date
- How many days each teaser precedes its article
- License
- Substack and LinkedIn assignment per post (assigned here for a weekly pairing, open to change)
