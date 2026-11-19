# GovernedRuntime
**File:** /README.md
**Description:** Reference implementations for a 24-post engineering series on governing autonomous AI agents at runtime.
**Author:** Libor Ballaty <liborballaty@gmail.com>
**Created:** 2026-11-18

## What this is

The series builds one system in the order an implementer would have to think about it. Every article
solves one problem on the way and has a code module here that implements the solution. The article
explains the problem and the design. The module is the working reference you can read, run and test.

Principle: an agent action is a privileged system event, not a conversational output. Control comes
from deterministic mechanisms outside the model (OS boundaries, short-lived credentials, inline
authorization, tamper-evident logs), never from prompts.

Auditability is not an afterthought. The ledger and tracing are built second, and no later module is
complete unless it records its decisions there.

## Status language

| Status | Meaning |
|---|---|
| `planned` | Listed in the content plan. No code yet. |
| `scaffolded` | File exists, interface sketched, not working. |
| `implemented` | Works on the developer's machine. Tests exist. |
| `tested` | Tests pass on a stated OS and Python version. Limits documented. |

Nothing is called "production-ready". Modules are reference implementations until stated otherwise.
Each module README records the OS it was run on, what was run, and the known limits.

## Layout

- `docs/architecture.md`: target architecture at v1.0, shared contracts, and system state after each post
- `docs/content-plan.md`: the 24-post plan, formats, teasers, module map and open decisions
- `modules/00_audit/`: audit ledger and tracing, built second and used by everything after
- `modules/01_sandbox/`: runtime sandboxing, local model isolation and non-human identities
- `modules/02_gateway/`: MCP proxy, schema integrity, routing and failure containment
- `modules/03_compliance/`: policy, action tiers, clause mapping, reports and tenant isolation
- `examples/`: end-to-end examples and manifests

## Per-post requirements

Each post ships with: the module at its planned path, a runnable demo, tests including at least one
negative or attack case, audit events and trace IDs emitted and asserted in tests (from post 2 on), a README section (what it does, the threat addressed, known limits), and a
git tag `post-NN` so the article links to a stable snapshot.

## License

Not yet chosen.
