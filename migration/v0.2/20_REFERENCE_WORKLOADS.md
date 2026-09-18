# Reference Workloads

**Status:** modular v0.2 preparation draft  
**Purpose:** define architecture-level workload families and tier semantics used to stress, compare, and validate the system.

---

## Purpose of Reference Workloads

Reference workloads are not marketing demos and are not independent forks of the platform.

They exist to:

- expose missing abstractions;
- stress capability/module composition;
- reveal latency/reliability/security conflicts;
- test deployment flexibility;
- force realistic failure/degraded-mode design;
- evaluate reuse across materially different applications.

The architecture must support at least the seven workload families below.

Each family must eventually be developed into **three complete, production-meaningful reference systems**, yielding at least 21 reference systems.

Research may add additional orthogonal workloads when strong evidence shows they expose an important architectural dimension not covered here.

---

## Tier Model

Final tier names may be improved during research, but their semantics must remain approximately:

### Tier A — Focused / Lean Production

A deliberately narrow or highly prioritized system that is still genuinely useful in real life.

Tier A is **not**:

- a toy;
- a diagnostic-only harness;
- a hello-world;
- an intentionally crippled demo.

It should minimize unnecessary feature breadth while preserving a coherent, productive use case.

### Tier B — Representative / Full

A broader serious everyday/productive system representative of what a capable user might reasonably expect from the workload class.

Tier B should exercise more composition, persistence, reliability, integrations, and complex workflows than Tier A without intentionally maximizing every feature.

### Tier C — Ambitious / Hard Mode

A high-integration system intentionally designed to stress architectural boundaries.

Tier C may combine advanced orchestration, concurrency, multimodality, long-lived state, background work, adaptation, specialized controllers, and challenging failure/recovery behavior.

It should remain technically meaningful rather than adding complexity for spectacle alone.

---

## Required Definition Per Tier

For every tier of every workload, research should define enough detail to evaluate the architecture independently.

At minimum, capture:

- purpose;
- primary users/use context;
- scope;
- non-goals;
- representative user journeys;
- required capabilities;
- optional capabilities;
- expected module composition;
- state requirements;
- memory requirements;
- tool requirements;
- realtime/latency expectations;
- quality requirements;
- deployment assumptions;
- relevant resource classes;
- security/trust requirements;
- failure modes;
- degraded modes;
- recovery behavior;
- observability requirements;
- evaluation suite;
- acceptance criteria;
- architectural dimensions stressed;
- reusable capabilities/modules;
- major differences from the previous tier.

Avoid vague tier descriptions that cannot act as architecture tests.

---

## Reference Workload Families

### 1. Coding Agent

Stresses:

- code understanding;
- editing;
- tools;
- planning;
- verification;
- long-running work;
- environment interaction;
- context management;
- project instructions;
- test/debug loops;
- version control;
- error recovery;
- potentially subagent/delegation patterns.

Tier A should demonstrate that a deliberately minimal coding harness can still be fully productive rather than a toy.

Tier B should represent a broader serious coding workflow.

Tier C should stress ambitious engineering orchestration without requiring every possible feature to exist merely for complexity.

Research should derive the concrete tier systems from evidence rather than cloning one existing coding product.

---

### 2. Research Assistant

Stresses:

- retrieval;
- evidence quality;
- provenance;
- synthesis;
- source comparison;
- uncertainty;
- long-horizon investigation;
- research planning;
- claim tracking;
- persistent knowledge;
- contradiction handling;
- experiments/analysis where relevant.

The three tiers should progress from a focused but genuinely useful research workflow through a broad research system to an ambitious long-running research environment.

---

### 3. Persistent Personal Assistant

Stresses:

- long-term state;
- initiative;
- scheduling;
- memory;
- personalization;
- continuous operation;
- task continuity;
- notifications/reminders;
- tools/integrations;
- context switching;
- recovery after downtime;
- permission boundaries.

Keep this workload distinct from the Social Companion: practical assistance may overlap with social behavior, but neither should automatically collapse into the other.

---

### 4. Social Companion

Stresses:

- personality;
- identity continuity;
- autobiographical continuity;
- relationships;
- affect;
- social state;
- initiative;
- conversational naturalness;
- memory;
- multimodal presence;
- routines;
- interruption/turn-taking.

#### Tier A fixed concept: Bedside Companion

Tier A must be designed around a focused, genuinely useful **Bedside Companion** living locally on or near a smart display/device at the bedside.

This concept is intentionally more constrained than other tier definitions because it is a real desired deployment, not merely an abstract benchmark.

Required/likely capabilities for research to refine:

- 3D avatar using VRM-compatible assets;
- ASR;
- TTS;
- vision;
- conversational LLM;
- tool use;
- scheduled/cron behavior;
- selected persistent memory and conversational continuity;
- local device control where useful, such as display power/brightness and volume;
- companion-like morning/night routines;
- personal waking behavior that can assess whether the user is actually awake rather than merely firing an alarm.

**Home automation is not a Tier-A Bedside Companion requirement.**

This workload is intentionally limited to bedside/near-device use; it does not need room-scale or house-scale complexity.

##### Candidate physical platform

An older Android phone-class device is available for full repurposing and experimentation, making Android a particularly interesting candidate platform.

Research must not assume that all inference fits locally.

A practical architecture may combine:

- very small local VAD/ASR/vision/embedding/classifier/support models where feasible;
- local avatar/device-control logic;
- cloud or LAN-hosted conversational intelligence;
- offloaded TTS or other components when local quality/compute is inadequate.

The exact split remains a research decision.

#### Tier B and Tier C

Design progressively broader and more ambitious social companion systems while preserving modularity and avoiding unnecessary coupling to the Bedside Companion implementation.

---

### 5. Embodied AI VTuber / AI Performer

Acts as a high-complexity integration workload.

Potential stressors include:

- persistent runtime;
- streaming ASR;
- voice;
- multimodal perception;
- multiple speakers;
- speaker attribution;
- proactive and reactive interruption;
- targeted intercept;
- low-latency reactions;
- audience awareness;
- personality continuity;
- social relationships;
- autonomous initiative;
- background cognition;
- game interaction;
- tool use;
- avatar control;
- gaze;
- expression;
- gesture;
- OBS/stream control;
- subtitles;
- music-production interaction;
- world/game state;
- realtime controllers;
- degraded operation;
- 2D/3D/VRM-related embodiment adapters;
- external application/protocol control.

The workload should generate reusable modules rather than forcing AI-VTuber-specific assumptions into the core.

#### Embodiment/control architecture stress

Reference designs should exercise the distinction between:

- avatar engine/renderer/target;
- supported target action surface;
- controller;
- protocol/application adapter;
- high-level cognitive intent;
- fast control policy.

A controller must only expose/effect actions supported by the connected target.

Research should consider interoperable control layers such as VMC-compatible adapters where appropriate, while keeping protocol specifics outside the core.

VLA-style control should be conceptualized broadly enough to share abstractions with non-avatar embodied agents when appropriate.

---

### 6. Ambient Environment / Home-Automation Agent

This workload is distinct from the Bedside Companion.

It stresses wider environment understanding/control, potentially including:

- Home Assistant / HAOS integration;
- rooms/zones/entities;
- sensors;
- actuators;
- occupancy/presence;
- time/schedules;
- multi-user identity;
- permissions;
- local-first execution;
- privacy;
- network/device outages;
- graceful degradation;
- background cognition;
- proactive behavior;
- voice interaction;
- coexistence with deterministic automations/rules;
- physical-world consequences;
- safety constraints;
- auditability.

Tier A should still be a real useful home/environment system rather than a demo.

Tier C may approach an ambitious "JARVIS-style" ambient agent, but research must translate that cultural shorthand into explicit technical requirements rather than importing fictional capabilities.

---

### 7. Interactive Desktop / Computer Agent

Stresses:

- screen/GUI perception;
- browser/application control;
- files;
- cross-application workflows;
- tool/API vs visual execution decisions;
- recovery from UI/environment drift;
- artifacts;
- stateful long-running tasks;
- verification;
- approvals;
- safety boundaries;
- potentially background/parallel work;
- multi-agent orchestration.

#### Tier A

A focused, genuinely productive computer agent with a carefully prioritized capability set.

It should be simple enough to expose whether the platform can support a lean desktop agent without immediately becoming an overgrown office suite.

#### Tier B

A broader cross-application work system capable of serious multi-step productivity workflows, artifact creation/manipulation, browser/files/app interaction, and robust task continuation.

Research may study contemporary computer-work products as evidence/prior art but should derive the tier from requirements rather than clone a product.

#### Tier C

An ambitious desktop-work environment that may include:

- multi-agent orchestration;
- parallel/background work;
- persistent projects;
- adaptive tool selection;
- cross-application workflows;
- skill creation;
- interactive teaching;
- learning/programming from demonstration;
- procedure/task induction;
- workflow generalization;
- verification;
- recovery;
- long-lived work context.

**Learning from demonstration is a Tier-C capability cluster, not a separate workload that must itself be artificially split into three tiers.**

Research should investigate relevant approaches such as Programming/Learning from Demonstration and modern agentic workflow induction.

---

## Cross-Workload Capability Stressors

The workload program should deliberately reuse capabilities across families and identify whether apparently similar needs are genuinely the same abstraction.

Important cross-cutting stressors include:

- memory and state;
- capability/provider routing;
- interruption/preemption;
- multimodality;
- streaming;
- tool use;
- background cognition;
- scheduling;
- identity/persona;
- permissions;
- observability;
- deployment portability;
- degraded operation;
- model/provider replacement;
- instruction/context artifacts;
- extension/contribution surfaces;
- module-level routing;
- human-in-the-loop approval;
- proactive behavior;
- learning/adaptation.

A capability reused by several workload families is a strong candidate for generic platform support, but reuse must be proven rather than forced by naming similarity.

---

## Composition Principle

Reference systems should preferably be composed from reusable capabilities/modules rather than implemented as forks.

Higher tiers should often build on lower-tier capability sets, but tiering does not require strict inheritance if research finds a better composition model.

Workload-specific modules are allowed when the function is genuinely workload-specific.

The core must not become a collection of hardcoded special cases for the seven reference workloads.

---

## Evaluation Use

The 21+ reference systems should be used throughout architecture research to ask:

- Can this requirement be expressed cleanly?
- Which core abstractions are shared?
- Which modules are reusable?
- Which requirements conflict?
- Does the execution model scale down and up?
- Do realtime paths coexist with background cognition?
- Are extensions/routing observable?
- Can providers/models be replaced?
- Are failure/degraded modes coherent?
- Are security/permission boundaries expressible?
- Does the architecture remain understandable?

A plausible architecture is not sufficient if it only supports one workload elegantly and forces the others into special-case hacks.
