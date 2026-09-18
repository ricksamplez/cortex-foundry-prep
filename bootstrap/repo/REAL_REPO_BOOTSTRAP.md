# Real Research Repository Bootstrap Design

**Target repository:** `ricksamplez/cortex-foundry`

This document defines the minimal seed state to create **before** the first real Research run.

The repository name identifies the research program/repository only. It must not be treated as the future system name.

## Bootstrap principle

Seed only what is needed to:

- establish authoritative requirements;
- orient the first run;
- provide durable state/checkpoint locations;
- prevent context loss;
- let the Research run design/evolve the deeper Vault structure itself.

Do **not** pre-build a giant final ontology/taxonomy before research begins.

## Initial canonical files

### Root

- `README.md`
- `PROJECT_CONTEXT.md`

### Stable project docs

- `docs/00_CORE_REQUIREMENTS_CHARTER.md`
- `docs/10_RESEARCH_PROGRAM_CONTRACT.md`
- `docs/20_REFERENCE_WORKLOADS.md`
- `docs/30_KNOWLEDGE_AND_WORKSPACE_GOVERNANCE.md`
- `docs/40_RESEARCH_COMPLETION_AND_HANDOFF.md`

These should initially match the approved modular preparation drafts.

### Minimal state

- `state/CURRENT_STATE.md`
- `state/NEXT_WORK.md`
- `state/OPEN_QUESTIONS.md`

These are tiny initial state files, not permanent giant ledgers.

The Research run may replace `OPEN_QUESTIONS.md` with an index + sharded structure when appropriate.

## Directories the Research run may create/evolve

The first run is explicitly allowed to design/add structure such as:

- research/evidence;
- sources/ledgers;
- ontology;
- capabilities;
- modules/concepts;
- architecture/specifications;
- decisions/ADRs;
- experiments;
- evaluations;
- workload analyses;
- helpers/tools;
- generated indexes;
- archive.

These are **not** all required as empty bootstrap folders.

Avoid committing empty ceremony.

## Run-specific material excluded from initial Research repo state

Do not initially seed:

- Implementation Harness Setup Runbook;
- dedicated implementation-host inventory;
- Architecture Review Runbook;
- milestone-review issue templates specific to that later run;
- implementation-harness credentials/configuration.

Those artifacts should be introduced only when their phase begins.

## Obsidian

The repository may be opened as an Obsidian Vault.

Do not require committed local UI state.

A later `.gitignore` may ignore machine/user-specific Obsidian workspace files while allowing portable useful configuration if desired.

The Research run may decide the exact Obsidian configuration after establishing the Vault model.

## Git history objective

The real repository should begin with a coherent bootstrap commit rather than a long chain of preparation-only edits.

Preparation/migration history belongs outside the real Research repo.

After bootstrap, Research commits should represent meaningful durable research/workspace progress.
