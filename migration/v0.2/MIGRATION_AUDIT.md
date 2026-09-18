# v0.2 Migration Audit

**Status:** Phase 1/2 draft migration audit — passed  
**Source:** frozen v0.1 charter + accepted post-v0.1 preparation decisions

## Source verification

The attached frozen v0.1 source was independently re-read from the local uploaded file during this audit.

Verified:

- size: `44,635` bytes;
- SHA-256: `8b2731602fd968c046045c49b1fd194c432f594dc171cb1482137b987c7335c4`;
- numbered top-level source sections: `62`;
- first numbered section: `1. Mission`;
- final numbered section: `62. Final Research Directive`.

This matches `planning/BASELINE.md`.

## Structural migration checks

| Check | Result |
|---|---:|
| v0.1 section map entries | 62 |
| unique v0.1 section numbers | 62 |
| missing source sections | 0 |
| duplicate source sections | 0 |
| explicit dropped sections | 0 |
| mapped destination references | 70 |
| broken destination file/anchor references | 0 |

## Post-v0.1 decision checks

| Check | Result |
|---|---:|
| persisted decision IDs | 30 |
| unique decision IDs | 30 |
| decisions still pending integration | 0 |
| mapped decision destination references | 35 |
| broken decision destination references | 0 |

## Scope-isolation checks

| Check | Result |
|---|---:|
| preparation-workspace name/URL leaks in future-facing draft docs | 0 |
| explicit `GPT-6 Pro` identity mentions in Research Program Contract | 0 |
| explicit `GPT-6 Pro` identity mentions in Architecture Review Runbook | 0 |

Target implementation-model names remain allowed where they are technically relevant.

## Draft file-size sanity check

Approximate character counts:

| Draft | Characters |
|---|---:|
| Core Requirements Charter | 21,539 |
| Research Program Contract | 16,482 |
| Reference Workloads | 13,348 |
| Knowledge & Workspace Governance | 11,923 |
| Research Completion & Handoff | 9,509 |
| Implementation Harness Setup Runbook | 16,391 |
| Architecture Review Runbook | 7,297 |

No draft currently exhibits pathological giant-file growth.

These are not final permanent size thresholds; the research program remains required to establish its own measurable file-size/complexity policy.

## Non-trivial semantic migration cases

The following areas were intentionally **strengthened, split, or superseded** rather than copied mechanically:

- **§6 Smallest Adequate Intelligence:** retained while allowing effective end-to-end cost/reliability to matter rather than treating nominal model size as the only optimization.
- **§11 Routing/Allocation/Scheduling:** strengthened with module/capability-level workflow routing while retaining global observability.
- **§18 Reference Workloads:** expanded from five workload families to seven and requires three production-meaningful tiers per family.
- **§23 Ontology:** strengthened with canonicalization/collision semantics and new module-extension entity relationships.
- **§31 Research Autonomy:** strengthened with durable non-blocking open-question handling.
- **§36 CI Permission:** strengthened to container-first execution for WebUI runs, GitHub Actions only when justified, and heavy accelerator work deferred.
- **§46 Architecture Freedom:** strengthened with an explicit boundary that the research-program/repository name is not the system name.
- **§48 Codex Baseline:** owner later replaced the former CachyOS/Arch host assumption with a dedicated Ubuntu 26.04.1 LTS implementation laptop; Codex v0.153.4 remains a leading harness baseline, while the harness itself may be replaced with strong evidence.
- **§53 Subagents:** strengthened with effective-cost selection and a hard prohibition on using local/external project-test models as implementation-agent subagents.
- **§57 Review Issues:** strengthened to permit zero-to-many deduplicated/actionable issues per milestone review campaign.
- **§58 Research Stages:** implementation-harness setup and independent architecture review were moved into separate run-specific contracts instead of universal research context.
- **§60 Completion Criteria:** strengthened and reordered so research completes and prepares a handoff before the separate implementation-harness setup finalizes the execution environment.

## Important retained owner deltas

The modular draft explicitly retains, among other additions:

- project-only-memory/repository-authoritative research workflow;
- model-name hygiene for research/review runs;
- external Git repository and public skill-registry research;
- sparse/curated first-party skill policy;
- bounded knowledge files and deterministic sharding/rotation;
- dedicated Ubuntu implementation host and software baseline;
- Codex as leading but replaceable harness candidate;
- effective-cost-aware subagent selection;
- implementation-subagent boundary;
- Luna-only ChatGPT OAuth project-test rule;
- approved external/local test-provider boundaries;
- guaranteed-capacity-only Provider Capacity Snapshots;
- feature/modality-aware Model Suitability Knowledge Base;
- seven reference workload families and 21+ tier systems;
- Bedside Companion Tier-A concept including Huawei P30/Android candidate;
- Desktop Agent Tier-C learning-by-demonstration capability cluster;
- extensible instruction/context artifacts beyond `AGENTS.md`;
- explicit module extension/contribution surfaces;
- avatar target/action-surface/controller separation;
- module-level serial/parallel/conditional routing;
- production-quality reference/template modules;
- milestone-only architecture reviews with implementation paused;
- zero-to-many issue creation per review campaign.

## Naming audit

The modular draft treats the research-program/repository name only as a research identity.

The future system remains unnamed.

The research run may deliberately select a suitable canonical system name later, with rationale and basic collision checks.

## Result

**Phase 1 / Phase 2 migration status: PASS for the current draft.**

This does not mean the documents are immutable.

It means the current modular draft has passed the agreed structural and semantic loss-prevention checks and is suitable as the basis for Phase 3 Project Docs design.

Future edits must preserve the same no-loss invariant and should rerun equivalent checks.
