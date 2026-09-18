# Core Requirements Charter

**Status:** modular v0.2 preparation draft  
**Scope:** system-level invariants and requirements only. Research process, workspace governance, implementation-harness setup, and architecture-review procedures live in separate contracts.

---

## Mission

Design and specify a modular cognitive systems platform capable of composing heterogeneous AI/ML models, conventional algorithms, deterministic controllers, tools, external services, human input, and other capability providers into persistent agentic and companion systems.

The platform must support substantially different applications through reusable components rather than forcing each application into an independent fork.

The architectural ambition is comparable to constructing a software-defined artificial cognitive system from specialized functional components rather than relying on one monolithic general-purpose model. This is functional inspiration, not a claim that the system reproduces biological human cognition.

The research program/repository name is **not** the name of the system being designed. Until a deliberate canonical system name is selected, use neutral terms such as `the system`, `the platform`, or `the runtime`.

---

## Core Architectural Invariants

### Fundamental modularity

The platform must be fundamentally modular.

Cognitive capabilities, models, memory strategies, tools, perception systems, routing strategies, controllers, embodiment systems, schedulers, providers, and other functionality must be replaceable where technically reasonable.

The core should remain as small and capability-neutral as practical. Intelligence should primarily live in replaceable components rather than being hardcoded into the core runtime.

### Capability-oriented architecture

Consumers should depend primarily on **capabilities and contracts**, not specific models or implementations.

A capability such as `interaction.floor.intercept` must not intrinsically mean `run model X using runtime Y`.

Multiple providers may satisfy the same capability and may differ in implementation, model family, modality, programming language, hardware requirements, latency, quality, cost, reliability, locality, privacy, and execution modes.

Capabilities should remain comparatively stable while implementations remain disposable and replaceable.

---

## Heterogeneous Capability Providers

The platform must not assume that every intelligent function is best implemented by an LLM.

Potential capability providers include, non-exhaustively:

- frontier LLMs;
- small language models;
- VLMs;
- VLA models;
- speech-to-speech models;
- ASR and TTS models;
- audio/video understanding models;
- embedding models and rerankers;
- classifiers;
- reward models;
- world models;
- diffusion or flow models;
- pose models;
- graph models;
- time-series models;
- reinforcement-learning policies;
- learned controllers;
- conventional machine learning;
- probabilistic models;
- symbolic systems;
- constraint solvers;
- search and optimization algorithms;
- deterministic algorithms;
- state machines;
- native controllers;
- external services;
- tools;
- remote agents;
- human operators.

The architecture must remain extensible to model or intelligence classes that do not yet exist.

Provider descriptions should therefore favor capabilities and properties over a closed enumeration of model types.

---

## Smallest Adequate Intelligence

The system should favor the **smallest adequate intelligence** for a task.

This does not merely mean the smallest adequate LLM.

A deterministic algorithm, classifier, specialized neural model, SLM, larger model, external service, or other mechanism should be selected according to actual functional and quality requirements.

Escalation to more capable, slower, or more expensive intelligence should be possible when justified.

The architecture should permit hierarchical/cascading strategies where appropriate.

"Smallest adequate" must not be interpreted as blindly minimizing parameter count, reasoning effort, or nominal model tier when a slightly more capable configuration reduces failures, retries, end-to-end latency, or effective cost.

---

## Polyglot and Language-Neutral Contracts

The architecture must not require all modules to use one programming language.

A deployment may combine components written in Python, Rust, C/C++, Go, TypeScript, Java, or other suitable languages.

Language choice belongs to the implementation. Contracts belong to the platform.

Cross-language interoperability, serialization, IPC, ABI boundaries, RPC, shared memory, and related mechanisms must be selected according to latency, safety, portability, complexity, and deployment requirements.

Extremely latency-sensitive components must not be forced through expensive interoperability mechanisms merely to preserve uniformity.

---

## Deployment and Compute Scaling

The same logical cognitive system must operate across substantially different hardware configurations without requiring architectural rewrites of cognitive modules.

At minimum, support a continuum from:

### Serial constrained execution

Tasks run largely sequentially on limited hardware.

### Heterogeneous semi-parallel execution

CPU, GPU, NPU, and other available accelerators execute suitable work concurrently where beneficial.

### Highly parallel local execution

Multiple local accelerators/workers may execute many independent cognitive processes concurrently.

### Distributed execution

Compute may come from additional local machines, remote GPU machines, rented accelerators, cloud inference, remote accelerator nodes, or external providers.

Parallelism should primarily be an execution property rather than a cognitive-module implementation assumption.

---

## Hardware Neutrality

No currently owned GPU or machine is the architectural target.

Consumer hardware may be useful benchmark/deployment profiles, but poor performance on one device must not artificially constrain the architecture.

The system should support profiles spanning constrained local systems, consumer workstations, large-memory accelerators, multi-GPU systems, hybrid local/remote execution, and distributed compute.

### Hardware absence, simulation, and emulation

Lack of a physical device must not automatically remove an important capability from evaluation.

When required hardware is unavailable, use an appropriate simulator/emulator/digital test environment where doing so can exercise the real software contracts, protocols, control surfaces, and failure behavior with useful fidelity.

Examples may include:

- robots/embodied systems in Unity, Unreal Engine, or other suitable robotics/simulation environments;
- simulated sensors/actuators;
- emulated mobile/edge devices when real devices are unavailable;
- simulated smart-home devices connected to the real automation software stack.

Prefer **real surrounding software plus simulated missing hardware** over replacing the entire integration with a fake when the real software can reasonably run.

Simulation/emulation limitations and remaining hardware-only validation gaps must be explicit rather than silently treated as equivalent to physical testing.

---

## Execution and Resource Abstraction

The research must determine an execution abstraction capable of understanding resource characteristics and workload requirements.

Relevant resource dimensions may include:

- CPU capacity;
- GPU compute;
- VRAM;
- RAM;
- NPU capacity;
- memory bandwidth;
- accelerator topology;
- transfer overhead;
- network latency;
- cloud cost;
- model residency;
- cold-start cost;
- concurrency;
- batching efficiency;
- deadlines;
- jitter;
- power constraints;
- privacy constraints;
- reliability.

Modules should declare what they require and support rather than directly assuming a particular machine or accelerator whenever practical.

---

## Routing, Allocation, and Scheduling

Routing, resource allocation, and runtime scheduling are related but distinct concerns.

At minimum, investigate responsibilities equivalent to:

### Capability resolution

Which providers are technically capable of satisfying the request?

### Candidate selection

Which capable implementation is desirable under current constraints?

### Admission control

Can a candidate satisfy its required deadline, budget, reliability, privacy, or other constraints?

### Resource allocation

Where and with what configuration should it execute?

### Runtime scheduling

When should it execute relative to concurrent work?

Further decomposition is permitted when research supports it.

---

## Routing Latency

Routing must be extremely fast on latency-sensitive paths.

Routing overhead must be measurable as part of end-to-end latency.

A sophisticated router that consumes a material fraction of a task's latency budget is unacceptable when a faster policy can achieve adequate quality.

Different paths may use different mechanisms, including exact lookup, cached decisions, deterministic policies, cheap scoring models, learned routers, or expensive reasoning only when genuine ambiguity justifies it.

Hard realtime or near-realtime paths must be capable of precomputed or deterministic routing where appropriate.

---

## Module-Level Routing and Workflow Composition

Routing/orchestration must be expressible at module/capability granularity rather than existing only as one global top-level model router.

The architecture must be capable of representing useful execution compositions including:

- serial paths;
- parallel paths;
- fan-out / fan-in;
- conditional branches;
- cascades;
- fallbacks;
- speculative paths;
- feedback loops;
- cross-module routing.

Local/module routing freedom must preserve enough global observability for resource allocation, scheduling, cancellation, tracing, deadlines, failure handling, and resource accounting.

Working principle: **local routing freedom, global observability**.

---

## Adaptive Resource Allocation

Investigate a deterministic, observable, data-driven resource allocator capable of improving placement/configuration decisions from accumulated runtime measurements.

Relevant measured properties may include:

- p50/p95/p99 latency;
- jitter;
- throughput;
- CPU/GPU/NPU utilization;
- memory pressure;
- transfer overhead;
- cold-start behavior;
- batch efficiency;
- quality;
- monetary cost;
- failure probability;
- energy use where relevant.

Optimization must remain inspectable and reversible.

No optimizer may silently weaken security, safety, privacy, reliability, logging, or evaluation requirements merely to improve benchmark scores.

---

## Time Scales and Cognitive Lanes

The architecture must support functionality operating on different time scales.

At minimum, investigate distinctions comparable to:

### Realtime

Examples include VAD, interrupt handling, conversational floor control, streaming audio, fast avatar reactions, gaze, immediate controllers, and preemption.

### Interactive cognition

Examples include conversational reasoning, task decisions, tool use, social reasoning, response generation, and local planning.

### Background cognition

Examples include memory consolidation, reflection, deep research, long-horizon planning, evaluation, optimization, and dataset processing.

Slow cognition must not unnecessarily block fast reactions.

---

## Multi-Source Perception

The platform must support multiple independent perception streams of the same modality when applications require them.

For visual perception, named streams may include desktop/screen capture, camera feeds, self/mirror views, environment cameras, application-rendered views, or future sources.

Streams should be independently configurable and individually enableable/disableable.

The architecture should preserve source identity/provenance and allow stream-specific:

- sampling/rate;
- preprocessing;
- privacy/access policy;
- latency budget;
- provider/model routing;
- retention;
- quality/resolution;
- downstream subscribers.

Different streams must not be forced through one model/provider or one cadence.

Optional cross-stream fusion should be possible without erasing the independent provenance or control of each source.

---

## Interruption and Proactive Intercept

The system must distinguish passive interruption from proactive interception.

Passive interruption may involve stopping output because another participant begins speaking.

Proactive intercept may involve:

- speaker identification;
- tracking conversational floor state;
- detecting a salient or urgent statement;
- deciding whether interruption is socially appropriate;
- selecting the intended participant;
- timing the interruption;
- acquiring the conversational floor;
- preempting current speech/cognition when justified.

This capability is an important stressor for low-latency social cognition.

User-observed behavior from external systems may be recorded as such until a suitable primary public source is captured; observation status must not be silently upgraded into stronger evidence.

---

## Event, State, Idempotency, and Replay

Latency and idempotency are high-priority engineering properties.

The architecture must support, where relevant:

- traceability;
- correlation and causation;
- cancellation;
- retries;
- duplicate handling;
- safe replay;
- event/schema evolution;
- deterministic behavior where determinism is required;
- graceful failure;
- degraded operation.

Do not apply one delivery/consistency policy universally. Determine per flow whether semantics such as at-most-once, at-least-once, effectively-once, transactional, replayable, or ephemeral behavior are appropriate.

---

## Long-Lived Operation

The platform must support persistent systems that may operate for long periods.

Relevant concerns include:

- restart recovery;
- state restoration;
- checkpointing;
- health monitoring;
- memory continuity;
- provider failure;
- model replacement;
- degraded modes;
- hot reconfiguration where appropriate;
- rolling upgrades;
- operator intervention;
- disaster recovery.

---

## Profiles, Composition, and Extension

Reference systems should preferably be compositions of reusable capabilities/modules rather than independent forks of the runtime.

Composition mechanisms such as layering, overlays, profiles, inheritance-like configuration, or other approaches should be researched rather than predetermined.

### Module extension and contribution model

Modules must be able to extend other modules through explicit, versioned extension/contribution surfaces.

At minimum, keep the following relationships semantically distinct:

- `requires` — depends on a capability;
- `provides` — supplies a capability;
- `extends` / `contributes` — adds behavior, actions, data, or integration to an explicit extension point.

Do not default to deep OOP-style module inheritance that creates hidden coupling.

Extension relationships should be observable, versionable, conflict-resolvable, and capability-driven where practical.

Conditional contributions should be possible when the presence of capabilities/providers changes what an extension can expose.

The architecture should distinguish dependency, capability, extension/contribution, execution, and data/event relationships even if their physical representation is not a graph database.

---

## Controller and Target Action Surfaces

For embodied or controllable targets, controllers should consume an explicitly exposed supported action surface rather than assume every possible action exists.

The effective action space should be constrained by both:

- what the controller can issue;
- what the target/engine/device actually supports.

An avatar engine/renderer may expose state, rendering, animation, and supported avatar actions while remaining useful independently for preview, asset loading, playback, or inspection.

A complete interactive avatar profile normally composes a target/engine with one or more controllers.

Protocol/application adapters such as VMC-compatible integration or application-specific control layers should be possible without forcing those protocols into the core.

Controller abstractions should be broad enough that suitable VLA/control policies can potentially operate other embodiments, including robots or simulated entities, when an appropriate observation/action adapter exists.

### 3D avatar asset interoperability

The embodiment/avatar layer must support real-world avatar assets without tying the core to one authoring ecosystem.

At minimum, implementation must provide a sound path for:

- VRM models;
- VRChat-ready Unity avatar packages (`.unitypackage`).

PMX/MMD assets are an additional explicit interoperability target and should work cleanly where technically practical.

Format-specific import/conversion/runtime concerns should live behind adapters or bounded integration layers rather than leak into generic cognitive contracts.

Implementation should validate interoperability using representative real assets and textures when provided, not only synthetic placeholder geometry.

---

## Module System Requirements

Every reusable module must have a canonical identity and explicit contracts.

The module system must support enough metadata and semantics to reason about:

- capabilities provided/required;
- inputs/outputs;
- state requirements;
- supported execution modes;
- hardware/resource requirements;
- latency class;
- concurrency;
- idempotency;
- dependencies;
- privileges/security properties;
- lifecycle/version compatibility;
- extension points/contributions;
- routing/workflow composition;
- observability/evaluation hooks.

The exact manifest/schema format is a research decision.

---

## Module Lifecycle

Define a module lifecycle capable of distinguishing concepts comparable to candidate, experimental, supported, stable, deprecated, and retired.

Exact states may differ if research produces a stronger model.

Promotion should be evidence-based.

Deprecated modules must not silently disappear while existing profiles, historical experiments, or compatibility commitments depend upon them.

---

## Reference and Template Modules

The finished project should ship a small, curated set of production-quality demo/template/reference modules that genuinely help future module authors.

They should demonstrate important module-system patterns rather than toy code.

Collectively, the smallest useful set should teach relevant combinations such as:

- capability provision/consumption;
- stateful behavior;
- streaming;
- extension points/contributors;
- routed/composite behavior;
- tests;
- observability;
- configuration/lifecycle;
- required module documentation.

The exact module set and whether a scaffold/generator is warranted are research decisions.

---

## First-Party Skills

The system may ship first-party agent skills where a skill is genuinely the right abstraction, but the default should be **sparse and curated**, not a large undifferentiated skill dump.

Shipped skills must be purposeful, documented, versioned, security-reviewed, and consistent with the broader module/capability architecture.

A skill discovered during research is only a **candidate**. Before it becomes part of the implemented/shipped system, the implementation phase must evaluate it against the actual architecture, security model, maintenance quality, and current requirements and may modify, replace, or retire it.

---

## Context and Instruction Artifact Extensibility

Project/agent context handling must not hardcode `AGENTS.md` as the only meaningful instruction/context artifact.

Potential formats/roles include, non-exhaustively:

- `AGENTS.md`;
- `SOUL.md`;
- `USER.md`;
- `DESIGN.md`;
- other current/future vendor or project formats.

Research an extensible discovery/parsing/resolution model that can support:

- artifact type/semantics;
- directory scope;
- inheritance;
- precedence;
- overrides;
- conflict detection;
- includes/excludes;
- lazy loading and context budgeting;
- provenance;
- update/file watching;
- complex multi-file handling.

Semantically different artifacts must not be flattened into one undifferentiated instruction blob when those distinctions matter.

New formats should preferably be addable through adapters/resolvers rather than requiring core rewrites.

---

## Provider and Protocol Compatibility

The architecture should support multiple provider interaction styles where technically and contractually supported, including:

- local model runtimes;
- OpenAI-compatible APIs;
- provider-specific APIs;
- streaming protocols;
- Responses-style APIs;
- Chat-Completion-style APIs where relevant;
- officially supported OAuth/subscription-backed provider routes.

Responses-style interaction should be considered independently from traditional Chat Completions.

Where officially supported, subscription-backed provider usage may be investigated as one provider option.

Unsupported credential extraction, token theft, or undocumented authentication bypasses are unacceptable.

---

## Controlled Optimization and Improvement

The platform should support controlled continuous improvement without allowing optimization loops to rewrite trust assumptions unchecked.

Potentially optimizable elements may include:

- model selection;
- routing;
- prompts;
- context construction;
- reasoning budgets;
- sampling;
- memory policy;
- tool policy;
- workflow graphs;
- module selection;
- hardware placement;
- caching;
- fine-tunes/adapters;
- training data;
- distillation.

Improvements should follow a process broadly equivalent to:

`observe → evaluate → propose → sandbox → benchmark → compare → approve/promote → monitor → rollback`

The exact mechanism is a research decision.

Security boundaries, trust roots, permission enforcement, audit integrity, update authority, and evaluation integrity must not be optimized away.

---

## Security, Trust, and Governance

Security controls must remain outside untrusted optimization loops where appropriate.

Investigate and specify:

- least privilege;
- module permissions;
- sandboxing;
- secrets handling;
- provider trust;
- supply-chain risk;
- unsafe external skills/plugins;
- authenticated control;
- auditability;
- rollback;
- operator emergency control.

No optimization/self-improvement mechanism may gain credit for better performance by weakening evaluation, logging, security, or safety controls.

---

## Versioning, Compatibility, and Evolution

Define a complete versioning and compatibility strategy before implementation matures.

Do not assume one version number is sufficient for the ecosystem.

At minimum, address:

- runtime/framework version;
- module version;
- module contract/API version;
- event/schema version;
- configuration schema version;
- ontology version;
- profile/bundle version;
- persistent-state/database schema version.

Determine and document:

- initial versioning convention;
- patch/minor/major semantics;
- breaking changes during pre-1.0 development;
- criteria for 1.0;
- prerelease policy;
- module-independent versioning where useful;
- compatibility rules;
- migration policy;
- deprecation process;
- support windows where applicable;
- schema evolution;
- ontology compatibility.

Where practical, tooling/CI should enforce versioning and compatibility rules rather than leaving them as prose only.

---

## Architecture and Naming Freedom

Working terminology such as "Mixture of Models", "Execution Fabric", "Capability Fabric", or "Cognitive Fabric" is provisional.

Research may replace terminology and architecture when evidence supports a clearer abstraction, provided all hard requirements remain satisfied and the reasoning is documented.

The research repository/program name is **not** the final system, runtime, framework, SDK, protocol, or product name.

A canonical system name may be proposed and selected once sufficient architectural identity exists.

Any final name should be deliberate, technically appropriate, reasonably distinct, and should avoid sloppy, throwaway, meme-only, or artificially grandiose naming. Before adoption, check obvious project/package/repository conflicts where practical.

Naming must not constrain architecture prematurely and may be reconsidered before it becomes an external compatibility surface.

Requirements matter more than current vocabulary.
