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

The program defines **seven** materially different workload families.

Every family must be developed into **three complete, production-meaningful reference systems**, yielding at least 21 reference systems.

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
- client/frontend model where relevant;
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

### Coding Agent

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

No concrete Coding-Agent tier implementation is fixed yet.

Research must design all three tiers according to the global tier semantics. Tier A should remain deliberately lean yet fully productive; Tier B should represent a broader serious coding workflow; Tier C should stress ambitious engineering orchestration without adding complexity merely for spectacle.

Existing systems may be studied as references, but the tier systems must be derived from requirements rather than cloned.

---

### Research Assistant

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

No concrete Research-Assistant tier implementation is fixed yet.

Research must design all three tiers according to the global tier semantics, progressing from a focused but genuinely useful research workflow through a broad serious research system to an ambitious long-running research environment.

---

### Persistent Personal Assistant

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

#### Tier A fixed direction: Smartphone Personal Assistant

Tier A must be deployable as a genuinely useful personal assistant on a smartphone.

Inference may be:

- fully local on sufficiently capable hardware;
- provided by a machine on the local network;
- provided by an external/cloud inference endpoint;
- split between local specialist models and remote general intelligence.

Fully local operation is a valid deployment profile when the device is capable enough; it is not a universal Tier-A requirement.

A constrained smartphone test target may be used to validate that a very small on-device model/runtime path can operate when technically feasible. This is a deployment-path test, not a requirement that low-end hardware provide the preferred production inference path.

#### Tier B and Tier C — Open design space

Research must design the broader tiers according to the global tier semantics.

---

### Social Companion

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
- interruption/turn-taking;
- progressively richer embodiment.

#### Cross-tier affect, speech, and embodiment dimension

Social Companion tiers should investigate affect/speech processing as composable capability routes rather than one mandatory monolith.

For human speech, each speaker/ASR stream may independently enable:

- transcript/text-based affect or emotion classification;
- audio/prosodic affect or emotion classification;
- shared-encoder, multitask, or audio+text fusion approaches where justified.

Not every stream must activate every route. Source identity and timing/provenance must remain available for optional fusion.

The AI character may use a separate context-aware affect estimator that can consume generated text plus compact dialogue/social/runtime state rather than only the literal spoken sentence. A capable general model may initially provide this function while production usage is captured; a smaller specialist may later take over routine cases when implementation-time evaluation demonstrates that it is adequate.

Affect is one optional control signal, not a universal avatar-action gateway. It may influence facial expression, affect-dependent micro-behavior, and speech rendering, while unrelated high-level/direct actions may flow from an LLM/tool call, VLA, controller, or other appropriate capability without passing through the affect classifier.

Expressive Social Companion speech requires controllable rendering; a TTS path limited to uncontrolled plain-text input is not sufficient where expressive voice is required. The generic speech contract should remain provider-neutral and may map to structured style/prosody parameters, natural-language instructions, inline tags, control tokens, reference/style embeddings, nonverbal vocalizations such as laughter/sighs/throat-clearing, or future mechanisms supported by the selected TTS.

Lip sync should be derivable from generated TTS audio and/or provider timing/phoneme/viseme information where available. Facial expression should remain behind the abstract avatar-control contract and may commonly map to standard/custom blendshapes.

When VLA-style control is justified by embodiment complexity, high-level intent may originate from an LLM or other cognition while the VLA/controller remains capable of immediate perception-driven reactions such as obstacle avoidance or safety stops without waiting for a new high-level instruction.

#### Tier A fixed concept: Bedside Companion

Tier A must be designed around a focused, genuinely useful **Bedside Companion** living locally on or near a smart display/device at the bedside.

This concept is intentionally more constrained than other tier definitions because it is a real desired deployment, not merely an abstract benchmark.

Required/likely capabilities for research to refine:

- 3D avatar;
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

This workload is intentionally limited to bedside/near-device use; it does not need room-scale or house-scale complexity.

##### Candidate physical platform

A Huawei P30 (`ELE-L29`) is available for full repurposing and experimentation, making Android a particularly interesting concrete candidate platform.

During implementation, this device is expected to remain physically connected to the implementation laptop with ADB enabled so installation, debugging, logging, control, and repeatable device-level testing can be automated.

The device may be freely modified/reconfigured for this use case.

Research must not assume that all inference fits locally. In particular, components such as TTS may reasonably be offloaded when local compute/quality would produce an unacceptable voice experience.

A practical architecture may combine:

- very small local VAD/ASR/vision/embedding/classifier/support models where feasible;
- local avatar/device-control logic;
- cloud or LAN-hosted conversational intelligence;
- offloaded TTS or other components when local quality/compute is inadequate.

A ready avatar asset may be supplied to the implementation workspace; avatar-authoring itself should not become an accidental prerequisite for validating the Bedside Companion runtime.

The exact split remains a research decision.

#### Tier B fixed direction: Persistent Companion with Optional Standalone VR

Tier B must be a broader serious social companion with richer continuity, initiative, multimodal interaction, memory, tools, and embodiment.

It must support **optional VR presence compatible with Meta Quest 3**, while remaining fully useful without VR.

The VR path must be a client running **directly on the Quest-class headset**, not a PCVR-only design.

The cognitive/backend services may run:

- on a PC/server on the same local network;
- on a remote server;
- or in another suitable backend deployment.

The frontend/backend boundary should allow the user to continue an existing interaction/session by putting on the headset during operation rather than starting a disconnected companion instance.

The VR client may expose additional spatial/embodied capabilities that are unavailable or unnecessary in the non-VR client, while preserving shared identity/session/memory continuity.

The VR implementation is not tied to one engine. Unity or Unreal Engine may be selected per reference implementation according to technical fit, and using different engines for different VR experiments/reference implementations is acceptable when that yields useful evidence.

#### Tier C fixed direction: Embodied AI VTuber / AI Performer

Tier C should use an ambitious persistent **Embodied AI VTuber / AI Performer** as the Social Companion hard-mode reference system.

Potential stressors include:

- persistent runtime;
- streaming ASR;
- expressive TTS/voice;
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
- external application/protocol control;
- long-running live-operation reliability.

##### Independent vision streams

Tier C must support multiple independent named vision streams rather than one undifferentiated visual feed.

Initial examples include:

- desktop/screen view;
- webcam view of the human/operator;
- mirror/self-view so the agent can perceive its own rendered appearance;
- additional future streams when useful.

Each stream must be individually enableable/disableable.

The architecture should preserve source identity/provenance and allow source-specific:

- sampling/rate;
- preprocessing;
- privacy policy;
- latency budget;
- model/provider routing;
- retention;
- fusion with other streams.

Not every stream must be sent to the same model or processed at the same rate.

The system should support optional cross-stream fusion without losing the ability to reason about streams independently.

##### Avatar renderer and interoperability stress

Tier C should validate more than one renderer/import strategy rather than forcing every avatar asset through one path.

At minimum, investigate/implement:

- a comparatively lightweight VRM-oriented renderer/runtime path;
- a heavier game-engine-backed renderer path capable of handling VRChat-style Unity avatar packages (`.unitypackage`) where appropriate.

PMX/MMD interoperability remains an additional explicit target where technically practical.

Implementation testing will have access to one owner-provided avatar available in VRM, VRChat Unity-package, and PMX/MMD representations together with textures/assets.

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

The Tier-C AI Performer should generate reusable modules rather than forcing performer-specific assumptions into the core.

---

### Ambient Environment / Home-Automation Agent

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

#### Tier A fixed direction: Greenhouse Agent

Tier A should be a focused, genuinely useful **Greenhouse Agent**.

It should exercise real environment sensing/control, schedules, automation coexistence, fault handling, and physical-world consequences without requiring whole-home scope.

Where Home Assistant semantics are part of the test, prefer a real Home Assistant OS instance with simulated/emulated devices rather than replacing Home Assistant itself with a fake. On the Ubuntu implementation host, a virtualized HAOS instance is the appropriate class of setup; Home Assistant Container is a distinct installation type and should not be treated as equivalent when HAOS-specific behavior matters.

#### Tier B and Tier C — Open design space

Research should expand from the greenhouse-scale environment into progressively broader ambient/home automation systems.

Tier C may approach an ambitious "JARVIS-style" ambient agent, but research must translate that cultural shorthand into explicit technical requirements rather than importing fictional capabilities.

---

### Interactive Desktop / Computer Agent

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

#### Tier A fixed direction: Application-Attached CoWork Agent

Tier A should be a focused, genuinely productive agent attached to **one specific application** and optimized for collaborative work inside that application's domain.

The intended pattern is one dedicated co-work agent per application rather than a general desktop controller pretending to understand everything.

It should be able to combine the application's available API/tool surface with visual/UI interaction where useful, maintain task context for that application, verify work, recover from ordinary UI drift, and remain intentionally lean enough to expose whether the platform supports high-quality application-specific agents without overbuilding a universal office suite.

#### Tier B — Fixed direction, open detailed design

A broader cross-application work system capable of serious multi-step productivity workflows, artifact creation/manipulation, browser/files/app interaction, and robust task continuation.

Research may study contemporary computer-work products as evidence/prior art but should derive the tier from requirements rather than clone a product.

#### Tier C — Fixed direction, open detailed design

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


Research should investigate relevant approaches such as Programming/Learning from Demonstration and modern agentic workflow induction.

---

### Embodied Agent / Robotics

This workload covers agents/controllers that act through embodied virtual, simulated, hardware-in-the-loop, or physical action spaces.

It stresses:

- VLA and other perception-action policies;
- sensor fusion;
- continuous/low-latency control;
- action-space negotiation;
- embodied state/proprioception;
- motion/planning/control separation;
- hard stop/preemption;
- safety constraints;
- simulation/emulation;
- simulation-to-real transfer;
- high-level cognition plus fast local control;
- partial hardware failure;
- actuator/sensor availability;
- deterministic safety boundaries;
- observability/replay of embodied actions.

#### Tier A fixed direction: Game / Virtual-World Agent

Tier A should be a genuinely useful embodied agent operating inside a game or virtual world.

It should exercise navigation, world state, object interaction, goals, perception/action loops, local reactions, and high-level cognition without requiring physical robotics hardware.

Unity 6.3 LTS (`6000.3.x`) and Unreal Engine 5.8.4 are both valid installed implementation/simulation environments. Engine choice should follow technical fit rather than a project-wide mandate.

#### Tier B fixed direction: Simulated Robotics / Digital-Twin Agent

Tier B should move into robotics-like sensing/control using a serious simulated robot or digital-twin environment.

It should add richer sensors/actuators, proprioception, continuous control, obstacle/environment handling, safety constraints, controller hierarchy, and VLA/learned-control evaluation where useful.

Unity, Unreal Engine, or another suitable robotics simulator may be used. Different experiments may use different engines when appropriate.

#### Tier C fixed direction: Physical / Hardware-in-the-Loop Robotics Agent

Tier C should validate the architecture against real physical robotics or hardware-in-the-loop behavior when suitable hardware becomes available.

It should stress real sensor/actuator timing, safety, partial hardware failure, jitter/latency, emergency-stop semantics, local fast control, slow cognition, and simulation-to-real gaps.

A physical robot is not currently available. Until one is available, implementation must maximize simulation/HIL coverage and explicitly preserve the remaining physical-validation gap rather than skipping the workload.

A general controller/action-surface abstraction should permit suitable controller families — including VLA-style controllers — to operate virtual agents, simulated robots, physical robots, avatars, or other embodiments through target-specific adapters.

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
- learning/adaptation;
- hardware simulation/emulation and explicit physical-validation gaps where hardware-dependent workloads require them.

A capability reused by several workload families is a strong candidate for generic platform support, but reuse must be proven rather than forced by naming similarity.

---

## Composition Principle

Reference systems should preferably be composed from reusable capabilities/modules rather than implemented as forks.

Higher tiers should often build on lower-tier capability sets, but tiering does not require strict inheritance if research finds a better composition model.

Workload-specific modules are allowed when the function is genuinely workload-specific.

The core must not become a collection of hardcoded special cases for the seven reference workloads.

---

## Evaluation Use

The completed tiered reference-system set — at least 21 systems across the seven workload families — should be used throughout architecture research to ask:

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
