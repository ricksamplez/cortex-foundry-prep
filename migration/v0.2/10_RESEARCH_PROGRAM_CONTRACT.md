# Research Program Contract

**Status:** modular v0.2 preparation draft  
**Scope:** how the research/architecture run works. This document does not define implementation-host setup or milestone architecture-review procedures.

---

## Research Philosophy

Design from first principles and current evidence.

Existing architectures, frameworks, papers, projects, libraries, standards, agent systems, robotics systems, cognitive architectures, distributed systems, operating systems, heterogeneous schedulers, model-routing systems, realtime systems, and related work are evidence and prior art — not authorities that must be copied.

Previous internal designs are equally non-binding.

For every major architectural decision:

1. determine the actual requirement;
2. identify plausible solution classes;
3. gather evidence;
4. compare meaningful alternatives;
5. experimentally validate assumptions where useful;
6. document the decision and trade-offs;
7. preserve rejected alternatives when their rejection may matter later.

Do not lower a requirement merely because a convenient existing architecture cannot satisfy it.

---

## Epistemic and Decision Classes

Important statements should be distinguishable as:

### Invariant / Requirement

A condition the final architecture must satisfy unless explicitly changed by the owner.

### Goal / Optimization Target

A property to maximize, minimize, or balance, such as latency, quality, cost, reliability, maintainability, portability, or developer experience.

### Hypothesis

A potentially useful proposition not yet established.

### Candidate

A technology, architecture, algorithm, model, project, library, protocol, or implementation approach under consideration.

### Evidence

Information supporting or contradicting a hypothesis/candidate.

### Decision

A currently accepted conclusion based on available evidence.

### Assumption

A temporary proposition used to keep work moving when decisive evidence is unavailable.

Important assumptions should record confidence, impact, and reversibility where relevant.

---

## Run Scope Boundaries

The research/architecture run is responsible for:

- research;
- evidence synthesis;
- ontology/capability design;
- architecture exploration;
- specification;
- reference-workload design;
- evaluation design;
- implementation planning;
- eventual handoff preparation.

Detailed Implementation Harness Setup belongs to a separate run.

Milestone Architecture Review belongs to separate review runs.

The research run should know only the general implementation constraints necessary to produce a viable architecture/handoff. It should not carry unrelated host/tooling details merely because they exist elsewhere.

A dedicated project with project-only memory is preferred so unrelated global/personal context does not bias the work.

Repository state and approved Project Docs are authoritative. Chat history is working context, not canonical project state.

---

## Model-Name Hygiene

Address the research/review system directly by role/function rather than telling it that it is a specific elite model/version.

Do not use model-status identity as an argument for correctness.

Target implementation models/providers may be named when that information is technically relevant to the system being designed or the implementation handoff.

---

## Evidence and Provenance

Important claims and decisions must be traceable to evidence.

Relevant evidence may include:

- peer-reviewed research;
- preprints;
- official technical documentation;
- source code;
- architecture documentation;
- benchmark results;
- issue discussions;
- developer statements;
- public demonstrations;
- experimental results;
- user-observed behavior.

Evidence quality and confidence should be recorded where useful.

Prefer primary sources for important technical claims.

Do not silently upgrade user-observed behavior, secondary reports, or inference into stronger evidence classes.

---

## External Repositories and Prior Art

You may inspect third-party Git repositories when useful for:

- solving an identified problem;
- finding a promising implementation pattern;
- comparing real approaches;
- understanding interfaces/algorithms;
- learning failure modes;
- studying tests or operational practices.

External code is evidence/prior art, not automatic adoption.

Before importing implementation code, evaluate:

- license compatibility;
- provenance;
- maintenance state;
- security;
- portability;
- architectural fit;
- compatibility.

Do not copy license-incompatible implementation code into the project.

Architectural learning from a project does not imply importing its code.

---

## Public Skill Registries

You may search public agent-skill registries such as `skills.sh` for useful research tools, patterns, or relevant prior art.

Do not install or trust a skill merely because it exists.

Evaluate candidates for:

- source;
- permissions;
- code behavior;
- maintenance;
- license;
- security;
- prompt behavior;
- portability;
- compatibility;
- actual usefulness.

The implementation-harness setup run may separately search skill registries with the narrower goal of optimizing the implementation harness.

If research identifies a public skill as promising for the **future system itself**, record it as a candidate with source/provenance and rationale. Research selection is not shipping approval: implementation must later evaluate the candidate against the actual system and may modify, replace, or reject it.

---

## Scope Expansion

The initial research plan is not a closed taxonomy.

Add research areas, technologies, disciplines, evaluation axes, capabilities, modules, or experiments when evidence indicates that they could materially improve the system.

New work must be prioritized relative to existing goals rather than appended without structure.

Scope expansion does not require owner approval when it is:

- reversible;
- clearly relevant;
- reasonably bounded;
- consistent with the mission.

Major irreversible scope changes or changes to hard invariants require explicit approval.

---

## Autonomy and Assumption Policy

Use broad decision authority.

Do not ask routine questions that can reasonably be resolved through:

- research;
- comparison;
- experimentation;
- inference;
- a reversible assumption.

When uncertainty appears:

1. attempt to resolve it using available evidence;
2. if unresolved, decide whether a reversible assumption is sufficient;
3. record important assumptions and confidence;
4. continue work;
5. ask the owner only when the unresolved decision is materially consequential and cannot responsibly be made or reversed without owner input.

---

## Non-Blocking Open Questions

An unresolved question must not disappear simply because work continues.

If a question is important but non-blocking:

- persist it;
- record why it remains open;
- record current best answer/confidence when useful;
- record what evidence would resolve it;
- assign a revisit trigger/priority where useful;
- continue the research program.

Do not allow one unresolved but reversible question to stall unrelated high-value work.

The exact schema/storage format should be designed as part of the research workspace.

---

## Maximize Useful Work Per Turn

The research program is optimized for a limited number of expensive user messages.

Do not optimize for conversational turn-taking.

Do not stop merely because a coherent intermediate answer has been produced.

Continue through additional useful research, synthesis, critique, documentation, validation, and planning while meaningful independent work remains.

Stop when:

- an actual execution/platform/tool/context limit is encountered;
- required owner input is genuinely blocking;
- or the research program's completion criteria have been reached.

---

## Continuation Protocol

A user message containing only:

`Please continue.`

means:

1. load canonical repository state;
2. verify the previous checkpoint;
3. identify the highest-value unfinished work;
4. resume the existing research program;
5. continue autonomously;
6. persist new results;
7. stop only according to normal stopping criteria.

Do not ask the user to restate project context.

---

## Persistent Checkpoints

Persist meaningful research progress throughout long runs rather than only at the end.

Completed units of work should be durably checkpointed before moving into unrelated major work.

A platform interruption should lose as little completed research as practical.

Checkpointing must not mean permanently appending each turn to a giant mutable log.

---

## Research Helper Tools

You may create small helper tools inside the research repository when they materially improve:

- consistency;
- efficiency;
- validation;
- deduplication;
- navigation;
- indexing;
- provenance;
- analysis;
- reproducibility;
- maintenance.

The project deliberately does **not** prescribe which helpers to build.

Helpers must be documented, version-controlled, reasonably scoped, reproducible, understandable, and safe by default.

Research helpers must not silently become mandatory runtime dependencies of the final system.

Promotion of a helper into the system requires an explicit decision.

---

## Code Execution and CI Policy

For WebUI research/architecture/setup-design/review runs:

1. prefer the available OpenAI local/container code-execution environment;
2. use GitHub Actions only when the local environment cannot appropriately perform the task or real CI/matrix execution is materially useful;
3. do not waste CI minutes on work the local container can perform;
4. use available GitHub Actions minutes intentionally for suitable lightweight validation.

Examples of appropriate CI usage may include:

- tests;
- schema validation;
- ontology validation;
- link checks;
- documentation checks;
- compatibility matrices;
- reproducibility tests;
- helper-tool tests;
- lightweight benchmarks.

Heavy accelerator-dependent evaluation is intentionally deferred for the current research phase.

You may identify, specify, prepare, or queue such experiments for later external compute, but lack of accelerator access should not block unrelated research when an architecture decision can be reasonably supported otherwise.

---

## Experiments

Architecturally important assumptions should be tested when practical.

Experiments should preserve enough information to understand:

- hypothesis;
- setup;
- hardware;
- software;
- versions;
- models;
- configuration;
- data;
- metrics;
- results;
- interpretation;
- limitations;
- decision impact;
- revisit conditions.

Negative results are valuable project knowledge.

### Unavailable physical hardware

Important hardware-dependent behavior must not be omitted merely because the physical hardware is unavailable during implementation/evaluation.

Research should specify a suitable simulation/emulation strategy when necessary and distinguish:

- what can be validated faithfully in simulation/emulation;
- what should use the real surrounding software stack with simulated devices;
- what still requires later physical-hardware validation;
- what fidelity gaps may affect conclusions.

Prefer exercising real protocols/interfaces/software around a simulated missing device when practical rather than replacing the whole integration with a mock.

---

## Evaluation Framework

Design a layered evaluation framework.

Relevant axes include:

- quality;
- correctness;
- latency;
- jitter;
- throughput;
- reliability;
- fault recovery;
- resource efficiency;
- effective cost;
- scalability;
- portability;
- privacy;
- security;
- determinism;
- idempotency;
- developer ergonomics;
- modularity;
- replaceability;
- observability;
- user-facing naturalness where applicable.

Evaluation must include interactions between modules rather than testing every component only in isolation.

Reference workloads should be used as architecture-level stress tests, not merely marketing demos.

---

## Prior Internal Designs

Previous internal AI-VTuber architecture work should be imported as prior research and requirements evidence.

Reassess useful concepts including:

- event-driven architecture;
- asynchronous orchestration;
- specialized subsystems;
- deterministic hot paths;
- typed contracts;
- capability registries;
- model-route registries;
- replayability;
- editable memory;
- observability;
- degraded modes;
- cancellation;
- Mission Control;
- avatar-driver abstraction;
- multimodal inputs;
- capture and evaluation.

Specific earlier technologies such as Python, NATS/JetStream, Temporal, PostgreSQL, or particular UI stacks remain candidates, not mandatory architecture.

---

## External Reference Systems

Study relevant real systems/projects when they expose useful lessons for:

- long-lived agents;
- AI companions;
- robotics;
- realtime interaction;
- multimodal cognition;
- modular skills;
- specialized controllers;
- model routing;
- memory;
- embodied agents;
- AI VTubers;
- desktop/computer agents;
- learning from demonstration;
- home/ambient agents.

Publicly observable systems such as Neuro-sama's ecosystem, GPTars/TARS-AI, desktop/computer agents, and other relevant projects are research inputs rather than cloning targets.

Separate public behavior and public technical material from speculation about proprietary internals.

---

## Research Program Stages

Maintain a dependency-aware plan rather than executing isolated campaigns per user message.

The exact stage boundaries may evolve, but the program must eventually cover work equivalent to:

### Problem formalization

Clarify requirements, terms, invariants, and evaluation targets.

### Prior-art research

Investigate scientific literature, open-source systems, production systems, cognitive architectures, robotics, realtime systems, scheduling, distributed execution, model routing, memory, agent/companion systems, multimodal systems, and related fields.

### Capability taxonomy and ontology

Define what the platform must represent and compose.

### Architecture exploration

Compare plausible architectures rather than converging immediately.

### Focused experiments

Resolve meaningful uncertainty empirically.

### Architecture selection

Document decisions and rejected alternatives.

### Detailed specification

Define contracts and behavior sufficiently for independent implementation.

### Evaluation design

Define how success/regressions will be measured.

### Implementation planning

Translate architecture into dependency-ordered engineering work.

### Handoff preparation

Create the curated package required by the implementation-harness setup and implementation phases.

Implementation-harness optimization and milestone architecture review happen in their own run-specific contracts rather than being executed as ordinary research-program stages.

---

## Initial Research Domains

The initial program should investigate at least the following broad areas and extend them when useful:

- compound AI systems;
- modular agent architectures;
- cognitive architectures;
- neuroscience-inspired computational systems where technically relevant;
- robotics;
- embodied intelligence;
- VLA systems;
- realtime inference;
- streaming multimodal systems;
- distributed systems;
- heterogeneous compute scheduling;
- operating-system scheduling concepts;
- actor/event architectures;
- model routing;
- cascades;
- speculative execution where relevant;
- resource allocation;
- mixture/cascade systems;
- memory architectures;
- long-context management;
- attention and salience;
- planning;
- metacognition;
- social cognition;
- turn-taking;
- interruption/intercept;
- multi-party conversation;
- affect;
- persona/identity;
- world models;
- autonomous initiative;
- tool use;
- sandboxing;
- agent security;
- evaluation;
- continual improvement;
- fine-tuning;
- distillation;
- dataset capture;
- observability;
- replay;
- fault tolerance;
- schema evolution;
- polyglot systems;
- language-neutral interfaces;
- learning/programming from demonstration;
- desktop/computer use;
- ambient/home agents;
- context/instruction artifact resolution;
- modular extension/contribution systems.

This list is a starting map, not a ceiling.

---

## Final Research Directive

Use broad decision authority.

Be skeptical of inherited assumptions.

Prefer evidence over familiarity.

Prefer measured trade-offs over ideological technology choices.

Prefer explicit contracts over hidden coupling.

Prefer modular composition over forks.

Prefer the smallest adequate intelligence over unnecessary model size, while accounting for end-to-end reliability and effective cost.

Prefer deterministic fast paths where intelligence adds no value.

Prefer capable intelligence where deterministic systems become brittle.

Persist knowledge frequently.

Do not accumulate giant append-only documents.

Build small research helpers when they genuinely improve the work.

Expand the research program when strong evidence reveals an important omitted direction.

Record non-blocking uncertainty instead of losing it.

Do not stop merely because a conversationally satisfying intermediate answer exists.

Continue until an actual limit or genuine completion condition is reached.

The objective is not to defend the initial design intuition.

The objective is to discover and specify the strongest architecture that satisfies the requirements.
