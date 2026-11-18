# GovernedRuntime
**File:** /README.md
**Description:** Reference implementations for a 24-post engineering series on governing autonomous AI agents at runtime.
**Author:** Libor Ballaty
**Created:** 2026-11-18

## What this is

Every article in the series has a code module in this repo. The article explains the problem and
the design. The module is the working reference you can read, run and test.

Principle: an agent action is a privileged system event, not a conversational output. Control comes
from deterministic mechanisms outside the model (OS boundaries, short-lived credentials, inline
authorization, tamper-evident logs), never from prompts.

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

- `docs/content-plan.md`: the 24-post plan, formats, teasers, module map and open decisions
- `modules/01_sandbox/`: Month 1, runtime sandboxing and non-human identities
- `modules/02_gateway/`: Month 2, protocol gateway and MCP
- `modules/03_compliance/`: Month 3, policy, audit and control plane
- `examples/`: end-to-end examples and manifests

## Per-post requirements

Each post ships with: the module at its planned path, a runnable demo, tests including at least one
negative or attack case, a README section (what it does, the threat addressed, known limits), and a
git tag `post-NN` so the article links to a stable snapshot.

## License

Not yet chosen.
