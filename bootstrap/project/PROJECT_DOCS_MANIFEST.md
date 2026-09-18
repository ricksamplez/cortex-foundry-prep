# Initial Project Docs Manifest

**Status:** preparation design for the dedicated project-only-memory Research Project.

The first Research run should receive stable, high-value project context without carrying Implementation Harness Setup or Architecture Review details.

## Project Docs to include

### 1. Project Context / Authority Index

Use `PROJECT_CONTEXT.md` as the small orientation document.

Purpose:

- explain what the research program is;
- clarify that the research-program/repository name is not the future system name;
- define document authority;
- define run-scope boundaries;
- point to the canonical stable documents;
- state that evolving project state belongs in the repository.

### 2. Core Requirements Charter

Source draft:

`migration/v0.2/00_CORE_REQUIREMENTS_CHARTER.md`

Contains system-level invariants and requirements.

### 3. Research Program Contract

Source draft:

`migration/v0.2/10_RESEARCH_PROGRAM_CONTRACT.md`

Contains evidence/autonomy/research-process rules.

### 4. Reference Workloads

Source draft:

`migration/v0.2/20_REFERENCE_WORKLOADS.md`

Contains the seven workload families and three-tier requirements.

### 5. Research Workspace & Knowledge Governance

Source draft:

`migration/v0.2/30_KNOWLEDGE_AND_WORKSPACE_GOVERNANCE.md`

Contains repository/Vault/ontology/documentation/model-suitability/capacity governance.

### 6. Research Completion & Implementation Handoff

Source draft:

`migration/v0.2/40_RESEARCH_COMPLETION_AND_HANDOFF.md`

Contains completion gates and handoff expectations.

## Do NOT include in the initial Research Project Docs

- Implementation Harness Setup Runbook;
- implementation-host software inventory beyond general architecture-relevant constraints;
- Architecture Review Runbook;
- review issue workflow details not needed by research;
- preparation-only migration artifacts;
- preparation-workspace names/URLs;
- unrelated personal/global user context.

Those documents belong to separate later chats/runs.

## Authority order

When documents appear to conflict:

1. latest explicit owner-approved requirement/change;
2. Core Requirements Charter for system invariants;
3. run-specific contract for behavior inside that run;
4. accepted ADR/spec in the canonical repository;
5. other research synthesis/evidence;
6. chat transcript.

A conflict must not be silently resolved by weakening a higher-authority requirement.

## Project-only memory

Use a dedicated Project with project-only memory.

The purpose is to isolate the research from unrelated personal/global context.

Project Docs and canonical repository state provide the intended persistent context.

## Progressive disclosure

The small Project Context document is orientation, not a duplicate charter.

The other Project Docs should remain directly available, while deeper evolving research should live in the repository and be loaded only when useful.

Do not duplicate the same canonical fact across several Project Docs merely to make it more visible.
