# Research Launch Candidate Package

**Status:** preparation-only owner review package  
**Purpose:** one compact checklist describing the exact candidate launch state for the first Research/Architecture run.

Nothing in this document authorizes writing to the real Research repository before the owner explicitly approves the launch/cutover.

---

## 1. Launch model

The first Research run should start inside a **dedicated ChatGPT Project with project-only memory**.

The Research run receives:

- stable Project Docs;
- concise Project Custom Instructions;
- access to the canonical Git repository;
- one first-run Research Start Contract.

The canonical repository becomes the evolving source of truth after the run starts.

Project Docs remain stable always-on mirrors/snapshots.

The preparation repository and its history must never be disclosed to the Research run.

---

## 2. ChatGPT Project Docs

Upload/add exactly these six stable documents to the Research Project:

1. `PROJECT_CONTEXT.md`
2. `00_CORE_REQUIREMENTS_CHARTER.md`
3. `10_RESEARCH_PROGRAM_CONTRACT.md`
4. `20_REFERENCE_WORKLOADS.md`
5. `30_KNOWLEDGE_AND_WORKSPACE_GOVERNANCE.md`
6. `40_RESEARCH_COMPLETION_AND_HANDOFF.md`

Preparation sources:

- `bootstrap/project/PROJECT_CONTEXT.md`
- `bootstrap/repo/seed/docs/00_CORE_REQUIREMENTS_CHARTER.md`
- `bootstrap/repo/seed/docs/10_RESEARCH_PROGRAM_CONTRACT.md`
- `bootstrap/repo/seed/docs/20_REFERENCE_WORKLOADS.md`
- `bootstrap/repo/seed/docs/30_KNOWLEDGE_AND_WORKSPACE_GOVERNANCE.md`
- `bootstrap/repo/seed/docs/40_RESEARCH_COMPLETION_AND_HANDOFF.md`

The five numbered docs are intentionally identical to their prepared real-repo seed counterparts except for their preparation-vs-canonical Status line.

`PROJECT_CONTEXT.md` is intentionally identical between the Project and prepared repo seed.

---

## 3. ChatGPT Project Custom Instructions

Use the complete contents of:

`bootstrap/project/CUSTOM_INSTRUCTIONS.md`

as the dedicated Research Project Custom Instructions.

Do not upload this file as a normal Project Doc.

Its responsibilities are behavioral:

- maximize useful completed work per expensive message;
- repository = canonical evolving state;
- Project Docs = stable always-on mirrors;
- research before asking routine questions;
- reversible assumptions instead of unnecessary blocking;
- persist non-blocking questions;
- checkpoint throughout long runs;
- preserve epistemic classes;
- container-first / GitHub-Actions-fallback execution;
- avoid giant append-only files;
- allow small research helpers;
- support `Please continue.` and `Continue.` recovery/intervention semantics;
- force fresh runs to begin substantive work rather than only planning.

---

## 4. Prepared initial canonical repository seed

The prepared seed currently contains **11 files**.

### Root

- `README.md`
- `PROJECT_CONTEXT.md`

### Stable requirements / research contracts

- `docs/00_CORE_REQUIREMENTS_CHARTER.md`
- `docs/10_RESEARCH_PROGRAM_CONTRACT.md`
- `docs/20_REFERENCE_WORKLOADS.md`
- `docs/30_KNOWLEDGE_AND_WORKSPACE_GOVERNANCE.md`
- `docs/40_RESEARCH_COMPLETION_AND_HANDOFF.md`

### Minimal state

- `state/CURRENT_STATE.md`
- `state/NEXT_WORK.md`
- `state/OPEN_QUESTIONS.md`

### Repo-only prior art

- `prior-art/ai_vtuber_v1_technical_blueprint_spec_PATCHED_v4_alpha_beta_roadmap.md`

The prior-art blueprint is available on demand and is **not** a Project Doc or architecture authority.

The first Research run is expected to evolve the deeper Vault structure instead of receiving dozens of empty pre-created directories.

---

## 5. Material deliberately excluded from the initial Research context

Do **not** seed/upload/inject:

- the preparation repository name or URL;
- migration maps/audits/history;
- preparation-only decision logs;
- Home Automation shopping shortlist;
- Implementation Harness Setup Runbook;
- dedicated implementation-host hardware/software inventory;
- implementation credentials/provider keys;
- Architecture Review Runbook;
- milestone review issue workflow details;
- preparation-only publication notes;
- unrelated personal/global user context.

Implementation/setup/review material enters only when its dedicated later phase begins.

---

## 6. First user message

Use the complete contents of:

`bootstrap/run/RESEARCH_START_CONTRACT.md`

as the first user message in the first Research chat.

Do not spend a separate expensive message testing repository/GitHub access.

The first Research turn itself must:

1. read/understand Project Docs;
2. inspect the canonical repository;
3. perform a short repository read/write preflight;
4. use a meaningful bootstrap/checkpoint write instead of disposable junk where practical;
5. if write access succeeds, continue immediately;
6. inspect the repo-only prior-art blueprint as needed;
7. establish/evolve the minimal scalable Vault;
8. create/update a dependency-aware research map;
9. persist state/open questions;
10. begin substantive research in the **same turn**.

If repository write access genuinely fails, that is a real blocker and should be surfaced.

---

## 7. Backend interruption / continuation workflow

Long Research turns may be interrupted by platform/backend limits.

A message containing only:

- `Please continue.`
- or `Continue.`

means:

1. rehydrate canonical repository state;
2. verify the last checkpoint;
3. select the highest-value unfinished work;
4. resume without asking for a recap.

### Continuation with owner intervention

The owner may instead send something like:

`Continue. <short correction / observation / constraint / priority change>`

The Research run should:

1. treat the addition as an intervention on the existing run;
2. classify whether it changes a requirement, assumption, decision, priority, or only local execution;
3. persist material changes in the appropriate canonical artifact;
4. update research state/backlog when necessary;
5. continue substantive work in the same turn.

Do not spend the whole continuation message merely acknowledging the intervention.

This workflow deliberately supports external owner review/monitoring between long Research bursts without resetting the research program.

---

## 8. Owner monitoring workflow

The owner may periodically inspect progress from outside the Research chat, especially when a long turn has already stopped because of backend/tool/context interruption.

No special Research turn is required merely for monitoring.

When external review discovers a problem, the owner can inject a short correction with the next `Continue.` message.

The Research run should rely on canonical repository state rather than expecting the external reviewer to reconstruct or paste the full context.

---

## 9. Initial reference-workload framework

The authoritative detailed specification is `20_REFERENCE_WORKLOADS.md`.

Current workload families:

1. Coding Agent
2. Research Assistant
3. Persistent Personal Assistant
4. Social Companion
5. Ambient Environment / Home-Automation Agent
6. Interactive Desktop / Computer Agent
7. Embodied Agent / Robotics

Each requires three production-meaningful tiers.

Do not duplicate the complete tier specification into prompts or run-local state; link back to the canonical workload document.

---

## 10. Current separation of phases

### Phase A — Research / Architecture

Uses the launch package described here.

### Phase B — Implementation Harness Setup

Separate chat/run.

Receives completed Research output and explicit GPT-6 Astra/host/harness context.

Its runbook is intentionally absent from Phase A.

### Phase C — Implementation

Begins only after Research completion + handoff + harness setup.

### Phase D — Milestone Architecture Review

Separate review chats at meaningful implementation milestones only.

Implementation is paused while a milestone review runs.

---

## 11. Remaining owner/manual actions before first Research run

After owner approval of the candidate wording:

1. create/configure the dedicated ChatGPT Project with project-only memory;
2. add the six Project Docs;
3. paste/set the prepared Project Custom Instructions;
4. populate the real Research repository with the approved 11-file seed as coherently as practical;
5. open the first Research chat inside the dedicated Project;
6. send the Research Start Contract as the first message.

Repository-access verification then happens **inside that first Research turn**, not as a separate message.

---

## 12. Current gates

### Passed

- v0.1 lossless migration mapping;
- post-v0.1 decision accounting;
- seed ↔ modular-draft synchronization;
- Project/Repo authority semantics;
- Project-Doc scope isolation;
- run-scope isolation;
- model-name hygiene;
- prior-art placement;
- final assistant editorial/consistency pass;
- leak/stale-reference checks;
- continuation/intervention workflow;
- first-turn repository preflight design.

### Still intentionally open

- owner final review/approval;
- actual real-repo bootstrap/cutover;
- actual ChatGPT Project creation/configuration;
- first Research run.

---

## 13. Owner approval meaning

An owner approval such as:

`Approved for launch.`

should mean:

- the current modular v0.2 candidate wording is accepted as the initial Research authority;
- the prepared 11-file real-repo seed may be used;
- the six Project Docs may be installed in the dedicated Project;
- the prepared Project Custom Instructions may be installed;
- the Research Start Contract may be used for the first Research chat.

Approval does **not** freeze future research.

The Research program remains explicitly allowed to discover better architectures, terminology, evidence, questions, and bounded scope expansions subject to the established requirements/change rules.
