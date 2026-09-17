# Cortex Foundry — Bootstrap Preparation Plan

**Purpose:** define the next preparation sequence before any real research run is launched.

This plan is preparation-only. Later runs must not receive references to this workspace.

---

## Phase 1 — Lossless charter modularization

Starting point: the frozen v0.1 charter identified in `planning/BASELINE.md` plus all post-v0.1 decisions in `planning/CURRENT_DECISIONS.md`.

Produce a modular successor while preserving every meaningful source requirement.

### Expected logical documents

The exact names may change during preparation, but the content should be separated approximately into:

1. **Core Requirements Charter**
   - mission;
   - architecture invariants;
   - heterogeneous intelligence;
   - polyglot requirement;
   - execution/compute requirements;
   - routing/allocation/scheduling;
   - long-lived operation;
   - module/extension model;
   - provider compatibility;
   - security/trust;
   - versioning/compatibility;
   - documentation requirements;
   - final architecture freedom.

2. **Research Program Contract**
   - research philosophy;
   - evidence/provenance;
   - decision classes;
   - external repo/skill research;
   - autonomy;
   - continuation protocol;
   - scope expansion;
   - helper tooling;
   - experiments/evaluation;
   - local-container-first execution policy;
   - non-blocking open questions;
   - completion behavior.

3. **Reference Workloads**
   - seven workload families;
   - three production-meaningful tiers each;
   - Tier-A Social Companion / Bedside Companion fixed concept;
   - Desktop/Computer Agent Tier-C apprenticeship/learning-by-demonstration capability family;
   - reusable module/capability stress dimensions.

4. **Research Workspace & Knowledge Governance**
   - repository authority;
   - Obsidian-compatible but portable knowledge model;
   - no-monster-files rule;
   - canonical ontology/deduplication;
   - Module Card + README standard;
   - Model Suitability Knowledge Base requirements;
   - Provider Capacity Snapshot requirements;
   - open-question persistence;
   - versioned/sharded/rotated append-only artifacts.

5. **Research Completion & Implementation Handoff Requirements**
   - research completion criteria;
   - curated implementation package requirements;
   - explicit Astra target where technically relevant;
   - handoff should not dump the entire research history into implementation context.

6. **Implementation Harness Setup Runbook** — separate run/chat only
   - GPT-6 Astra target;
   - Codex v0.153.4 leading baseline but replaceable with strong evidence;
   - supported ChatGPT OAuth constraint;
   - Ubuntu 26.04.1 dedicated host profile;
   - existing toolchain/software baseline;
   - plugins/skills/MCP/tool freedom;
   - issue tracking evaluation;
   - subagent roles/model/reasoning/cost selection;
   - no external/local implementation subagents;
   - project-test provider allowlist;
   - Luna-only ChatGPT OAuth project-evaluation rule;
   - reproducibility/security/approval setup.

7. **Architecture Review Runbook** — separate milestone review chats only
   - stable checkpoint/commit input;
   - implementation paused during review;
   - comprehensive milestone review;
   - zero-to-many issue creation;
   - finding deduplication/grouping;
   - spec-conflict path;
   - review completion criteria.

---

## Phase 2 — Migration map / loss proof

Create a migration map from every v0.1 section/content unit to its new canonical home.

Required properties:

- no silent deletion;
- explicit replacement markers where wording/semantics become stronger;
- post-v0.1 additions mapped separately;
- run-specific sections removed from universal context but not discarded;
- final audit for accidental preparation-workspace leakage.

The original frozen v0.1 must remain identifiable by SHA-256 from `planning/BASELINE.md`.

---

## Phase 3 — Project Docs design

Design only the documents that the initial Research run should see automatically.

Principles:

- minimal always-on context;
- progressive disclosure;
- Project Docs contain stable/high-value context, not transient logs;
- do not include Implementation Harness Setup details that are irrelevant to research;
- do not include Architecture Review instructions;
- do not identify the research model by elite model/version name;
- direct instructions toward `you` / role/function;
- repository remains canonical state.

---

## Phase 4 — Project Custom Instructions

Create concise behavior-level instructions only.

Likely requirements:

- maximize useful completed work per turn;
- use repo as canonical state;
- make and record reversible assumptions rather than blocking;
- persist meaningful checkpoints;
- continue until actual limit/completion;
- distinguish requirement/hypothesis/evidence/decision/assumption;
- do not silently weaken requirements;
- record non-blocking questions;
- use local WebUI code environment before GitHub Actions;
- avoid giant files;
- never treat chat transcript as canonical state.

Do not duplicate the architecture charter in Custom Instructions.

---

## Phase 5 — Actual research-repository bootstrap

Design the minimal seed state for `ricksamplez/cortex-foundry`.

The initial bootstrap should provide enough structure for the research run to start safely while allowing it to redesign/expand the Vault when justified.

Avoid overbuilding the final taxonomy before research begins.

Potential bootstrap categories to decide during preparation:

- canonical Project Docs;
- state/checkpoint files;
- source/evidence intake area;
- ADR/decision area;
- experiments area;
- helper-tool area;
- schemas/validation if already justified;
- archive/migration area.

The Research run should remain authorized to improve the structure.

---

## Phase 6 — Research Start Contract

Create the first user prompt/run contract.

It should:

- operationalize the Project Docs;
- instruct the model to inspect/initialize the repo;
- establish a dependency-aware research plan;
- begin real research in the same message rather than stopping after planning;
- permit external repos and public skill registries as evidence/prior-art sources;
- permit creation of small research helpers;
- establish frequent persistence/checkpoints;
- establish the `Please continue.` protocol;
- allow bounded relevant scope expansion;
- ensure questions that are not blocking are persisted and work continues;
- emphasize maximum useful work per expensive message.

It should **not** contain Implementation Harness host/setup details except where the eventual implementation target constrains architecture in a genuinely general way.

---

## Phase 7 — Pre-launch audit

Before the first real run:

- verify no v0.1 requirement disappeared;
- verify all post-v0.1 deltas are integrated;
- verify Research-run context excludes setup/review-only material;
- verify no preparation-workspace name/URL/reference leaked;
- verify no global/personal context is accidentally assumed;
- verify Project-only-memory plan;
- verify the actual research repo is ready;
- verify first prompt causes research to start immediately rather than only producing a plan.

---

## Immediate next action

Begin Phase 1: construct the modular charter successor and migration map in this preparation workspace before writing anything into the real research repository.
