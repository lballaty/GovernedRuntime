# GovernedRuntime Content Plan
**File:** /docs/content-plan.md
**Description:** Source of truth for the 24-post series: topics, platforms, teasers, code modules and status.
**Author:** Libor Ballaty
**Created:** 2026-11-18

Status: Draft. Series start date is not yet set, so weeks are relative (W1 to W12, two posts per week).

## Format rules

| Format | Use | Audience |
|---|---|---|
| Substack | Long-form canonical pieces with code walkthrough | Architects, engineers |
| LinkedIn article | Concept-led: threat model, compliance, strategy | CISOs, CTOs, risk owners |
| LinkedIn short | One module, one idea, link to repo | Broad reach |

Every Substack piece and every LinkedIn article gets a LinkedIn teaser post (18 teasers). LinkedIn short
posts are their own teaser. Totals: 24 content items, 42 publications.

## Month 1: Foundation (sandboxing and non-human identities)

| # | Wk | Title | Platform | Module | Status |
|---|---|---|---|---|---|
| 1 | 1 | Stop Treating AI Agents Like Team Members. Treat Them Like Unvetted Microservices | Substack | `modules/01_sandbox/sandbox_runner.py`, `strict_agent.sbpl` | planned |
| 2 | 1 | Ephemeral Capability Leases: Securing Non-Human Identities in Agentic Workflows | LinkedIn short | `modules/01_sandbox/token_broker.py` | planned |
| 3 | 2 | API-Driven vs Subscription-Driven Agents: Why the Threat Model Changes | LinkedIn article | `modules/01_sandbox/session_classifier.py` | planned |
| 4 | 2 | The Compliance Illusion: Why Policy Checkboxes Fail Under the EU AI Act | LinkedIn article | `modules/03_compliance/policy_mapper.py` | planned |
| 5 | 3 | Isolating Local SLMs: Ollama and MLX Behind Hard OS Boundaries | LinkedIn short | `modules/01_sandbox/local_slm_cage.sh` | planned |
| 6 | 3 | Revoking Access Instantly: Dynamic Capability Lease Invalidation | LinkedIn short | `modules/01_sandbox/lease_revoker.py` | planned |
| 7 | 4 | Local-First Economics of AI Inference vs Cloud Token Bloat | Substack | `modules/01_sandbox/cost_benchmark.py` | planned |
| 8 | 4 | Month 1 Architecture Review: Assembling the Foundation | Substack | `daemon.py` (phase 1, tag `phase-1`) | planned |

## Month 2: Gateway (protocol layers and walled gardens)

| # | Wk | Title | Platform | Module | Status |
|---|---|---|---|---|---|
| 9 | 5 | The Walled Garden: Governing Subscription-Driven Desktop Harnesses | LinkedIn article | `modules/02_gateway/mcp_config_interceptor.py` | planned |
| 10 | 5 | Intercepting JSON-RPC: An Inline Authorization Proxy for MCP | Substack | `modules/02_gateway/mcp_proxy.py` | planned |
| 11 | 6 | Model-Agnostic Fleet Routing Across Heterogeneous LLMs | LinkedIn article | `modules/02_gateway/fleet_router.py` | planned |
| 12 | 6 | Defending Against Tool Poisoning and Metadata TOCTOU | Substack | `modules/02_gateway/schema_validator.py` | planned |
| 13 | 7 | Cryptographic Schema Pinning: Stopping Upstream Description Drift in MCP | LinkedIn short | `modules/02_gateway/schema_pinning.py` | planned |
| 14 | 7 | Policy-as-Code in Agentic Data Loops | LinkedIn article | `modules/03_compliance/policy_evaluator.py` | planned |
| 15 | 8 | State Corruption and Cascading Failures in Multi-Agent Swarms | LinkedIn short | `modules/02_gateway/circuit_breaker.py` | planned |
| 16 | 8 | Month 2 Gateway Review: Hooking the Proxy to the Sandbox | Substack | `daemon.py` (phase 2, tag `phase-2`) | planned |

## Month 3: Enterprise control plane (auditability and scale)

| # | Wk | Title | Platform | Module | Status |
|---|---|---|---|---|---|
| 17 | 9 | The 3-Tier Action Matrix: Structuring Human-in-the-Loop Gating | LinkedIn article | `modules/03_compliance/action_matrix.py` | planned |
| 18 | 9 | Immutable Audit Ledgers: EU AI Act Traceability in Code | Substack | `modules/03_compliance/audit_sink.py` | planned |
| 19 | 10 | Governance for Multi-Tenant AI Backends | Substack | `modules/03_compliance/tenant_isolation_check.sql` | planned |
| 20 | 10 | Debugging Autonomous Loops: Tracing State Transitions Across Fleets | LinkedIn short | `modules/03_compliance/tracer.py` | planned |
| 21 | 11 | Non-Human Audit Trails: Proving Compliance to External Auditors | LinkedIn article | `modules/03_compliance/auditor_report_gen.py` | planned |
| 22 | 11 | Performance Overhead vs Security: Benchmarking the Gateway | Substack | `modules/03_compliance/benchmark_suite.py` | planned |
| 23 | 12 | The State of Enterprise AI: What Actually Works in Production | LinkedIn article | `examples/production_manifest.yaml` | planned |
| 24 | 12 | GovernedRuntime v1.0: End-to-End Orchestration | Substack | `daemon.py` (v1.0, tag `v1.0`) | planned |

## Open design flags (to settle before the posts they affect)

| Post | Flag |
|---|---|
| 1, 5 | Seatbelt denies operations, it does not strip syscalls. `sandbox-exec` is deprecated by Apple. macOS-only, so a Linux equivalent (bubblewrap, Landlock or seccomp) would widen the audience. |
| 2, 6 | The HMAC signing key must be unreadable from inside the sandbox. The broker runs as a separate process. |
| 3 | A process can classify a session by launch path and parent process. It cannot reliably identify a closed desktop app. State the limit. |
| 4 | Verify the EU AI Act clause mapping against the text. Articles 12, 14 and 19 (logging, human oversight, record-keeping) are likely more relevant than 5 and 50. |
| 7, 22 | Numbers come from measured runs with hardware and method stated. Cost figures cite a pricing source and date. |
| 9 | Rewriting `mcp.json` governs only servers launched from that file, not a client's built-in tools. State the boundary. |
| 10, all | Proxy port is not chosen. Avoid reserved local ranges used elsewhere. |
| 12, 13 | Keep both modules. Post 12 covers the attack and runtime validation, Post 13 covers pinning and manifests. |
| 19 | SQL and Postgres specific. Needs a test method. |
| 8, 16, 24 | `daemon.py` evolves. Tag each phase so each article links to a stable snapshot. |

## Open decisions

- Series start date
- Teaser timing relative to the article
- License
- Whether Post 2 should be a LinkedIn article instead of a short post
