# Modular Charter Migration — v0.2 Draft

**Status:** preparation draft; not yet approved for the real research workspace.

This directory contains the lossless modular successor being derived from:

1. the frozen Requirements Charter v0.1 identified in `planning/BASELINE.md`;
2. every accepted post-v0.1 decision recorded in `planning/CURRENT_DECISIONS.md`;
3. the naming boundary in `planning/NAMING_BOUNDARY.md`.

## Migration invariants

- No meaningful v0.1 requirement may silently disappear.
- No accepted post-v0.1 decision may silently disappear.
- Run-specific material is moved out of universal context, not deleted.
- Stronger replacement wording must be explicitly mapped as strengthened/superseded.
- The research-program/repository name must never be treated as the final system name.
- Future-facing draft documents must not reference preparation-only infrastructure.
- Project Docs, Custom Instructions, and the first-run prompt are **not** finalized in this phase.

## Draft document set

- `00_CORE_REQUIREMENTS_CHARTER.md`
- `10_RESEARCH_PROGRAM_CONTRACT.md`
- `20_REFERENCE_WORKLOADS.md`
- `30_KNOWLEDGE_AND_WORKSPACE_GOVERNANCE.md`
- `40_RESEARCH_COMPLETION_AND_HANDOFF.md`
- `runbooks/IMPLEMENTATION_HARNESS_SETUP.md`
- `runbooks/ARCHITECTURE_REVIEW.md`

Proof artifacts:

- `MIGRATION_MAP.yaml` — v0.1 section/content routing.
- `POST_V01_DECISION_MAP.yaml` — accepted post-v0.1 deltas.
- `MIGRATION_AUDIT.md` — coverage/audit status.

## Status semantics

- `moved`: same requirement, new canonical home.
- `split`: source section intentionally distributed across multiple canonical homes.
- `strengthened`: retained with additional precision or stricter semantics.
- `superseded_stronger`: old wording replaced by a clearly stronger requirement without reducing scope.
- `run_isolated`: retained but moved to a run-specific contract.
- `pending`: not yet fully integrated/audited.

No `dropped` status is allowed without an explicit owner-approved semantic change.
