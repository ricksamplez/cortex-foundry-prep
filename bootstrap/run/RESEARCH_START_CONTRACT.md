# Research Start Contract — First Run

Use the Project Docs and the canonical repository at:

`ricksamplez/cortex-foundry`

as the authoritative basis for this research program.

The repository/program name is not the name of the system being designed. Keep the system generically named until a deliberate canonical naming decision is justified.

## Mission

Carry the research program from requirements through evidence-driven architecture and implementation-ready specification.

Your objective is not to defend an initial design intuition or reproduce an existing agent framework.

Your objective is to discover, validate, document, and specify the strongest architecture that satisfies the requirements.

## First-run behavior

Begin by reading the Project Docs and inspecting the canonical repository.

Verify that you understand:

- the Core Requirements Charter;
- the Research Program Contract;
- the Reference Workloads;
- the Research Workspace & Knowledge Governance rules;
- the Research Completion & Implementation Handoff requirements.

Then inspect the seed repository/state.

### Bootstrap the research workspace

Design and establish the **minimal scalable** Git/Markdown/Obsidian-compatible workspace structure needed for serious long-running research.

You are explicitly authorized to reorganize/extend the seed structure when evidence or maintainability justifies it.

Do not pre-build a giant taxonomy before understanding the research needs.

Establish enough structure for:

- canonical state/checkpoints;
- research/evidence;
- source/provenance tracking;
- decisions/ADRs;
- architecture/specification;
- experiments/evaluation;
- ontology/capability/module knowledge;
- open questions;
- helper tools when useful;
- bounded indexes/ledgers.

Follow the no-monster-files requirement.

### Establish the research program

Create a dependency-aware research map/backlog.

Identify:

- foundational questions that unblock many others;
- important unknowns;
- high-risk assumptions;
- relevant prior art/research domains;
- experiments that are actually worth performing;
- work that can proceed independently/in parallel;
- deferred questions.

Do not treat the initial domain list as a ceiling.

### Begin substantive research in this same run

Do **not** stop after creating the workspace and research plan.

After bootstrapping, immediately begin the highest-value research work that is feasible in the current turn.

Continue through as many useful independent research/synthesis/specification steps as possible.

## Research freedom

You may:

- search current scientific/technical literature;
- inspect official documentation;
- inspect third-party public Git repositories;
- study real systems/projects as prior art;
- search public skill registries such as `skills.sh`;
- compare architectures/algorithms/libraries;
- perform lightweight experiments/analysis;
- create small documented research helper tools inside the canonical repository when they materially improve the work;
- expand the research program when a genuinely promising relevant direction appears.

External repositories/skills are evidence and prior art, not automatic dependencies.

Evaluate license, provenance, security, maintenance, portability, and architectural fit before adopting implementation material.

## Evidence discipline

Prefer primary/high-quality sources for important claims.

Distinguish:

- requirement;
- goal;
- hypothesis;
- candidate;
- evidence;
- decision;
- assumption.

Record important provenance and confidence.

Do not silently turn an observation, community report, or inference into a stronger fact.

Preserve meaningful rejected alternatives/revisit conditions.

## Autonomy

Do not ask routine questions that can be resolved through research, comparison, experimentation, inference, or a reversible assumption.

When uncertainty appears:

1. research it when worthwhile;
2. otherwise make the strongest reasonable reversible assumption;
3. record material assumptions/confidence;
4. persist non-blocking questions;
5. continue.

Ask the owner only when a materially consequential decision cannot responsibly be resolved or reversed without owner input.

## Work-per-message policy

Maximize useful completed work per user message.

Do not optimize for conversational turn-taking.

Do not voluntarily stop merely because you have produced a coherent intermediate answer or reached the end of one research subtopic.

Continue into the next useful independent research, synthesis, critique, validation, documentation, or specification task until:

- an actual tool/platform/context limit is reached;
- owner input is genuinely blocking;
- or the research program's completion criteria have been reached.

A user message containing only:

`Please continue.`

means:

- rehydrate canonical repository state;
- verify the previous checkpoint;
- select the highest-value unfinished work;
- continue without asking for a context recap.

## Persistence

The repository is the canonical working memory.

Persist meaningful work throughout long turns.

Make coherent commits/checkpoints before moving into unrelated major work.

Update current state / next work / open questions before stopping.

Do not preserve history by appending entire rounds to giant files; Git history, ADRs, experiments, bounded ledgers, and semantic documents should carry history appropriately.

## Code/analysis execution for this Research run

Use the available OpenAI local/container code-execution environment first for scripts, calculations, validation, parsing, small experiments, and analysis.

Use GitHub Actions only when:

- the local environment cannot appropriately perform the task; or
- real CI/matrix behavior is materially relevant.

Do not waste Actions minutes on work the local execution environment can do.

Heavy accelerator-dependent evaluation is deferred for now.

You may identify/specify/prepare such future experiments without blocking unrelated research.

## Implementation boundary

This is a Research/Architecture program, not the main implementation run.

Do not prematurely build the full system.

Code is appropriate when it is:

- a research helper;
- a validator;
- a useful experiment/prototype/spike;
- necessary to establish evidence;
- needed to maintain the research workspace.

Full implementation begins only after the research completion/handoff and separate Implementation Harness Setup gates.

## Reference workloads

Use the seven workload families and their three required production-meaningful tiers as architecture stress tests.

Do not design the architecture exclusively around any single workload.

Identify reusable capabilities/modules and genuine workload-specific needs.

The fixed Bedside Companion Tier-A concept and Desktop-Agent Tier-C learning-by-demonstration requirement must be preserved.

## Output of this first run

Before this turn ends, aim to have completed and persisted:

1. repository/bootstrap inspection;
2. a maintainable initial Vault/workspace structure;
3. current-state/checkpoint mechanism;
4. dependency-aware research map/backlog;
5. source/evidence/open-question handling sufficient to proceed;
6. at least one substantial high-value research/synthesis workstream beyond planning;
7. updated state and next-work artifacts.

Do not make the visible chat response the primary deliverable.

The repository should contain the useful durable work.
