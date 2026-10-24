# Cortex Foundry — Current Preparation Decisions

**Status:** active preparation decision ledger before Research cutover. Earlier "remaining work" sections may describe historical checkpoints; current launch status is tracked in `bootstrap/PRELAUNCH_AUDIT.md`.

This file records decisions made after the original v0.1 charter. It is preparation-only and is intended to prevent information loss while the final run-specific documents are designed.

---

## 1. Scope isolation and run structure

Later work should be split into separate runs/chats rather than one giant universal instruction set.

### Research / architecture run

Purpose:

- research;
- evidence synthesis;
- ontology/capability design;
- architecture exploration;
- specification;
- reference-workload design;
- evaluation design;
- implementation planning.

It should not carry detailed Implementation Harness Setup or Architecture Review instructions unless needed for handoff boundaries.

### Implementation Harness Setup run

Purpose:

- optimize the implementation environment specifically for GPT-6 Astra;
- treat Codex CLI as the leading baseline, not an immutable requirement;
- compare suitable alternative harnesses if evidence warrants it;
- design plugins, skills, MCPs, tools, subagents, model/reasoning allocations, context handling, issue workflow, security/approval behavior, and reproducible setup;
- target the actual dedicated implementation host.

### Architecture Review runs

Purpose:

- independent architecture/code review only at meaningful milestones;
- review stable commits/checkpoints;
- pause the live implementation agent while the review runs;
- generate zero-to-many validated GitHub issues in one review message/campaign where appropriate;
- avoid wasting one expensive review message on trivial changes.

### Project memory

The owner intends to use a dedicated ChatGPT Project with project-only memory so the research is not biased by unrelated personal/global context.

The repository and Project Docs are authoritative; chat history is transient working context.

---

## 2. Research autonomy and continuity

The research run should:

- maximize useful completed work per user message;
- continue through logically useful independent work until an actual hard/platform/tool/context limit or genuine completion condition is reached;
- resolve uncertainty by research first;
- otherwise make reasonable reversible assumptions, record them, and continue;
- ask the owner only when a consequential unresolved decision cannot responsibly be resolved or reversed;
- persist checkpoints throughout long turns;
- treat a bare `Please continue.` as a command to rehydrate canonical repo state and resume the highest-value unfinished work without asking for context again;
- record non-blocking open questions rather than letting them disappear;
- expand the research plan when a genuinely promising relevant direction appears.

Do not tell the research/review model that it is GPT-6 Pro. Address it directly by role/instruction. Target-model names are allowed when they are technically relevant to a handoff/setup task.

---

## 3. External research sources

The research run may inspect third-party Git repositories when useful for solving an identified problem or comparing real implementation approaches.

It may also search public skill registries such as `skills.sh`.

External code is evidence/prior art, not automatic adoption. License, provenance, maintenance, security, portability, architectural fit, and compatibility must be evaluated before reuse.

The project itself should ship first-party skills only sparingly and deliberately when a skill is genuinely the right abstraction.

---

## 4. Research workspace and helper tooling

The final research repository is expected to function as an Obsidian-compatible Git/Markdown knowledge Vault, but Git/portable files are the source format and no critical semantics may depend on fragile Obsidian-only plugins.

The research run may design the Vault structure itself.

It may create small local helper tools in the same repository when those materially improve consistency, validation, deduplication, navigation, provenance, analysis, reproducibility, or maintenance.

The prompt should not prescribe which helpers to build.

### No monster files

Do not permanently append every round to giant mutable files.

Prefer:

- current-state documents updated in place;
- semantic decomposition;
- Git history;
- ADRs;
- experiments;
- archives;
- sharded/rotated append-only ledgers.

The research run should establish a measurable file-size/complexity policy early enough to prevent pathological growth.

---

## 5. WebUI research/architecture/review compute policy

All GPT-6 Pro-style research, architecture, setup-design, and architecture-review runs occur in ChatGPT WebUI.

For code execution in those WebUI runs:

1. prefer OpenAI's available local/container code-execution environment;
2. use GitHub Actions only when the local environment cannot appropriately perform the task or real CI/matrix execution is materially useful;
3. do not waste CI minutes on work the local container can do;
4. heavy accelerator-dependent evaluation is intentionally deferred for now, though future experiments may be specified/prepared.

Available GitHub Actions minutes may be used for appropriate lightweight CI/validation work.

---

## 6. Dedicated implementation host

The actual implementation run will execute on a dedicated laptop rather than the main workstation.

Known host baseline:

- Ubuntu 26.04.1 LTS, fresh installation, dual boot;
- Intel i9-9980HK, 8C/16T, Turbo Boost disabled;
- 32 GB RAM;
- RTX 2070 8 GB;
- roughly 6–6.5 GB VRAM can be available in a lightweight/headless-ish environment;
- dedicated to the project so the owner's main workstation remains usable.

Known Codex security/approval baseline already proven usable for CUDA work:

- `sandbox_mode = danger-full-access`;
- `approval_policy = on-request`;
- `approvals_reviewer = guardian_subagent`.

This is an allowed known-good baseline for the dedicated host, not necessarily the final setup.

### Existing local development/runtime software

Installed baseline includes:

- Codex;
- Unsloth Studio (currently preferred for supported purely local model workflows);
- Ollama;
- llama.cpp;
- Blender 5.2.2 + MCP;
- Unity 6.6 + CLI + MCP;
- Unreal Engine 5.8.2 (linked into `~/.local/bin`) + MCP;
- `uv` + system Python;
- `nvm` + system Node;
- `gvm` for Go;
- `javm` for Java;
- `rustup` for Rust;
- Android SDK + emulator + docs;
- GCC / Clang / standard development toolchains;
- development and Ubuntu Server metapackages;
- Docker suite without Docker Desktop;
- Steam + Proton;
- `yt-dlp`;
- TwitchDownloaderCLI;
- Obsidian.

The setup run may extend this baseline. Native Linux is preferred when practical, but containers, Wine/Proton, or other compatibility approaches are permitted when justified.

The implementation run does not need GitHub Actions for ordinary local hardware/code execution; it has direct access to this substantially more capable host.

---

## 7. Implementation harness is not synonymous with Codex

Current leading baseline:

- GPT-6 Astra as main implementation model;
- Codex CLI v0.153.4 as the current known-good candidate because the owner's required experimental context-management behavior works there.

However, Codex itself is not an immutable requirement.

The Implementation Harness Setup run may recommend a different suitable harness (for example Hermes-Agent) only if there is a strong evidence-based reason and the owner can still use the ChatGPT subscription through an officially supported OAuth path.

The burden of proof for replacing the known Codex baseline should be high.

Experimental harness features are allowed but not mandatory.

---

## 8. Main-agent and subagent model selection

Astra Xhigh or Max are strong main-agent candidates for long-running implementation because community experience suggests that more reasoning can sometimes reduce expensive corrective loops. This is a hypothesis, not a guaranteed accounting rule.

Do not brute-force every model × reasoning-level combination. Prefer trustworthy public/community evidence and targeted validation for material uncertainties.

Subagent selection must account for **effective total cost**, not simply model size or reasoning label.

Relevant cost factors may include:

- subscription allowance consumption;
- scarce rolling/weekly-window pressure;
- monetary cost where applicable;
- latency/wall-clock time;
- failure probability;
- expected rework;
- orchestration overhead;
- opportunity cost.

A configuration such as Luna Max may be preferable to Terra Low if it is both cheaper in effective allowance terms and more reliable for that role.

Use the least expensive configuration that reliably achieves the required quality — not automatically the weakest or lowest-reasoning model.

### Hard boundary: implementation subagents

**The implementation harness itself must not use local models or external APIs as its own subagents/helpers.**

All main-agent/subagent intelligence used to implement the project must remain inside the approved ChatGPT-subscription/OAuth harness ecosystem.

Local models and external APIs outside the ChatGPT subscription exist **only for the project being built**, e.g.:

- module/provider integration tests;
- evaluations;
- experimental flows;
- capability tests;
- benchmark fixtures;
- project runtime/provider experiments.

They must not secretly augment the implementation agent's own reasoning workforce.

---

## 9. ChatGPT-subscription provider safety during implementation

If the project-under-test needs to exercise a ChatGPT subscription/OAuth provider during an Astra implementation run:

- use **GPT-5.6 Luna only**;
- allow Luna reasoning up to Max;
- do **not** use GPT-6 Astra as a project inference/judge/evaluation provider inside its own implementation run.

This prevents the implementation agent from consuming or deadlocking the same scarce Astra capacity it depends upon.

If an evaluation genuinely needs more intelligence, use an approved external project-test provider instead (for example an appropriate NVIDIA NIM endpoint such as Kimi K3, subject to current availability/limits).

`codex exec` may be exposed as one optional **Test Intelligence Provider** for project evaluations. It is not a substitute for subagents and receives no automatic preference over other suitable test providers.

---

## 10. Approved project-test inference resources

Existing accounts/credentials may be used by the project for evaluations/tests/provider work:

- Ollama Cloud Free (already configured on the implementation laptop);
- Groq Free;
- OpenRouter Free;
- NVIDIA NIM free endpoints;
- ChatGPT subscription/OAuth under the Luna-only rule above.

The Groq/OpenRouter accounts intentionally have no payment information, preventing accidental paid usage.

For OpenRouter:

- always use an explicit named model for reproducible evaluation;
- assume the free limits of a fresh account that has **not** received the post-$10-credit-top-up higher limits.

Local small models may also be used by the project. The laptop can comfortably host lightweight embeddings, classifiers, and other models that fit within roughly 6 GB usable VRAM, while much larger quantized/offloaded models may be usable only for slow background evaluation.

---

## 11. Provider Capacity Snapshot policy

Create a time-stamped provider-capacity representation rather than hardcoding rapidly changing provider limits into the permanent architecture.

Capture relevant guaranteed/normal account-plan constraints such as:

- RPM/TPM;
- daily limits;
- concurrency;
- rolling windows;
- 5-hour windows;
- weekly limits;
- monthly limits where applicable;
- model-specific restrictions;
- reasoning-specific restrictions;
- free-credit/quota state;
- reset semantics;
- source and checked-at timestamp.

**Do not include saved/banked resets or comparable opportunistic/non-guaranteed bonus capacity.**

Plan capacity is plan capacity. Bonus resets must never be treated as a dependable architectural resource.

---

## 12. Model Suitability Knowledge Base

The project should preserve reusable empirical guidance about model suitability at both capability and module/function level.

Record, when evidence supports it:

- adequate model-size/class range;
- when a larger class becomes necessary;
- known strong families;
- known weak/unsuitable families;
- quantization sensitivity;
- reasoning requirements;
- cost/latency implications;
- confidence and evidence;
- revisit conditions.

Suitability must also account for actual required **model capabilities**, not only intelligence/size, including for example:

- tool use/function calling;
- structured output / schema adherence;
- vision;
- image/video input;
- audio/speech input;
- speech/audio output;
- native multimodality;
- streaming;
- long context;
- embeddings/reranking where relevant;
- statefulness;
- realtime suitability.

Requirements may differ by feature within one module. An optional module function may legitimately require vision, speech, tool use, or a larger model even when the base function does not.

The knowledge representation should therefore support base requirements plus per-feature/optional-capability requirements instead of one simplistic `minimum_model_size` field.

---

## 13. Reference-workload tier philosophy

Every reference workload should eventually receive three fully developed systems.

Working tier semantics:

- **Tier A — Focused / Lean Production:** intentionally narrow/prioritized but genuinely useful in real life; not a toy or merely diagnostic system.
- **Tier B — Representative / Full:** broader serious everyday/productive system.
- **Tier C — Ambitious / Hard Mode:** high-integration architecture stress test.

Pi Agent is a useful mental example of Tier-A philosophy for coding: deliberately minimal, yet fully productive.

The final tier names may be improved by research.

---

## 14. Reference workload framework

The program now has seven fixed workload families with three production-meaningful tiers each:

1. Coding Agent
2. Research Assistant
3. Persistent Personal Assistant
4. Social Companion
5. Ambient Environment / Home-Automation Agent
6. Interactive Desktop / Computer Agent
7. Embodied Agent / Robotics

This yields at least 21 reference systems.

### Persistent Personal Assistant

Tier A fixed direction: **Smartphone Personal Assistant**.

It must be genuinely useful on a smartphone and may use fully local inference on sufficiently capable hardware, LAN-hosted inference, cloud/external inference, or a split local/remote architecture.

The Huawei P30 may be used as a constrained mobile test target. A tiny on-device model/runtime such as a Gemma4 E2B-class model via LiteRT-LM or a comparable mobile stack may be tested only to validate the local path; external/LAN inference remains the more realistic profile for this device.

### Social Companion

Current fixed anchors:

- Tier A: Bedside Companion;
- Tier B: Persistent Companion with optional standalone Quest-class VR client;
- Tier C: Embodied AI VTuber / AI Performer.

Tier B VR is **VR-capable, not VR-dependent**. The VR client runs directly on the headset rather than requiring PCVR, while backend cognition/services may run on a LAN PC/server or remote server. Session/identity/memory continuity should permit moving into VR during an active interaction instead of starting a disconnected companion instance.

### Ambient Environment / Home-Automation Agent

Tier A fixed direction: **Greenhouse Agent**.

### Interactive Desktop / Computer Agent

Current progression:

- Tier A: Application-Attached CoWork Agent;
- Tier B: broader serious cross-application work system;
- Tier C: ambitious multi-agent desktop work, background/parallel workflows, skill creation, learning from demonstration, interactive teaching, cross-application task induction, verification/recovery, etc.

### Embodied Agent / Robotics

Current progression:

- Tier A: Game / Virtual-World Agent;
- Tier B: Simulated Robotics / Digital-Twin Agent;
- Tier C: Physical / Hardware-in-the-Loop Robotics Agent.

Physical robot hardware is not currently available, so implementation should maximize simulation/HIL coverage and leave remaining physical-validation gaps explicit until hardware exists.

---

## 15. Social Companion Tier A — Bedside Companion

Tier A is intentionally more constrained than the other still-open tier definitions because the owner specifically wants this real system.

Concept:

A focused, genuinely useful bedside companion living on a smart display/device near the bed.

Required/likely characteristics for research to refine:

- 3D VRM avatar;
- ASR;
- TTS;
- vision;
- tool use;
- scheduled/cron behavior;
- selected persistent memory / conversational continuity;
- device control for its own/attached device where useful (e.g. display power/brightness, volume), **not a Home-Automation requirement**;
- small local perception/support models where practical;
- conversational LLM may be cloud-hosted or served from a local-network inference endpoint;
- intentionally limited room-scale scope because this remains Tier A.

### Candidate physical platform

An old Huawei P30 (`ELE-L29`) is available and may be fully repurposed/experimented on.

Android is therefore a particularly interesting candidate platform to research.

The device is compute-constrained enough that some work may need offloading — TTS is a likely example if local quality is poor.

### Important user-facing routines

Research should consider genuinely companion-like bedside routines rather than a generic alarm-clock wrapper, especially:

- Morning Routine;
- Go-to-Bed / nighttime routine;
- personalized waking;
- detecting whether the user is actually awake rather than merely firing an alarm and assuming success.

The exact wakefulness-detection implementation is intentionally not prescribed.

---

## 16. Ambient/Home-Automation workload remains distinct

The separate Ambient Environment / Home-Automation Agent remains a reference workload and may investigate HAOS/Home Assistant, sensors, rooms, actuators, multi-user permissions, physical-world consequences, and wider environment control.

Do not conflate that larger workload with the Bedside Companion's simple local device-control needs.

---

## 17. Agent/context instruction artifacts

Instruction/context handling must not hardcode `AGENTS.md` as the only meaningful project artifact.

Potential formats/roles include, non-exhaustively:

- `AGENTS.md`;
- `SOUL.md`;
- `USER.md`;
- `DESIGN.md`;
- other present/future vendor or project formats.

The architecture should research extensible discovery/parsing/resolution adapters that can support:

- artifact semantics/type;
- directory scope;
- inheritance;
- precedence;
- overrides;
- conflict detection;
- includes/excludes;
- lazy loading/context budgeting;
- provenance;
- file watching/update behavior;
- complex multi-file handling.

Different artifact types must not be flattened into one undifferentiated text blob if their semantics matter.

---

## 18. Module composition, extensions, and controllers

Modules may extend other modules through explicit, versioned extension/contribution surfaces.

Keep distinct concepts for:

- `requires` — depends on a capability;
- `provides` — supplies a capability;
- `extends` / `contributes` — adds behavior/actions/data to an explicit extension point.

Avoid accidental OOP-style inheritance tangles as the default composition mechanism.

Extension relationships should be observable, versionable, conflict-resolvable, and capability-driven where possible.

### Avatar engine / controller

Preferred current conceptual direction:

- Avatar Engine/Renderer exposes supported avatar state/action capabilities.
- Avatar Controller depends on/consumes the supported action surface.
- A complete interactive avatar profile normally composes engine/target + controller, but the engine should remain independently useful for rendering, preview, asset loading, animation playback, etc.
- effective controller action space is the intersection of controller capabilities and target/avatar capabilities.

Potential adapters/controllers may include VMC-based targets and application-specific integrations. VLA-style controllers should be conceptualized broadly enough that the same controller pattern could potentially drive non-avatar embodiments such as robots when an appropriate observation/action adapter exists.

---

## 19. Per-module routing and workflow composition

Routing/orchestration must be possible at module/capability granularity, not only as one global model router.

The architecture should permit meaningful compositions such as:

- serial;
- parallel;
- fan-out/fan-in;
- conditional branches;
- cascades;
- fallbacks;
- speculative paths;
- feedback loops;
- cross-module routes.

Local/module routing freedom must preserve sufficient global observability for scheduling, allocation, cancellation, tracing, deadlines, failures, and resource accounting.

Working principle: **local routing freedom, global observability**.

---

## 20. Demo/template modules

The finished project should ship a small curated set of production-quality demo/template/reference modules that genuinely help future module authors.

They should demonstrate important module-system patterns rather than toy code, potentially covering combinations of:

- simple capability provider;
- capability consumer;
- stateful behavior;
- streaming;
- extension points/contributors;
- routed/composite behavior;
- tests;
- observability;
- Module Card;
- `README.md`;
- configuration/lifecycle.

Do not prescribe an exact set prematurely. Research should determine the smallest set that teaches the module architecture well.

---

## 21. Architecture review and issue workflow

Architecture/code review should occur at meaningful milestones only.

During a review:

- pause the implementation run;
- review a stable commit/checkpoint;
- use relevant requirements/ADRs/evals/open questions;
- review the milestone comprehensively rather than stopping after the first finding;
- validate and deduplicate findings;
- create zero-to-many GitHub issues in one review campaign as appropriate;
- group related findings when one issue is the correct unit of work;
- keep independent fixes independent when needed.

Issues should be actionable and may include severity, affected requirement/ADR/contract/module, evidence, reproduction, expected/observed behavior, acceptance criteria, blocking status, and links/commit references.

Implementation evidence may reveal that the specification itself is wrong. The reviewer must allow explicit spec/architecture questions instead of assuming its previous decisions are infallible.

The Implementation Harness Setup run may investigate using GitHub Issues as a cross-run engineering control plane if that improves autonomy and traceability.

---

## 22. Historical immediate-work checkpoint — superseded

This section records the earlier bootstrap sequence for provenance. Most items have since been completed in the preparation workspace; current launch blockers and status are tracked in `bootstrap/PRELAUNCH_AUDIT.md`.

The earlier sequence was:


1. losslessly modularize the v0.1 charter;
2. integrate every persisted delta from this file;
3. create a migration/content map proving no requirement disappeared;
4. separate Research, Implementation Harness Setup, Handoff, and Architecture Review material;
5. design the Project Docs;
6. design minimal Project Instructions;
7. design the initial real-repo bootstrap;
8. design the Research Start Contract / first-run prompt;
9. define leak checks so preparation-only information cannot enter later run material;
10. only then initialize/populate the actual research workspace for the run.


---

## 23. Avatar renderer paths and owner-provided implementation fixtures

Avatar-format support is **not** a Cognitive-Core requirement.

The generic architecture must support replaceable avatar renderer/engine implementations behind stable embodiment/control contracts.

For the Social Companion / AI Performer reference path, current implementation targets are:

- a lightweight VRM-oriented renderer/runtime path;
- a heavier game-engine-backed renderer path capable of handling VRChat-style Unity avatar packages (`.unitypackage`) where useful;
- PMX/MMD interoperability as an additional explicit target where technically practical.

The owner has one matching avatar available in all three formats plus associated textures/assets.

During implementation, these files will be placed into a dedicated owner-provided Inbox/input directory in the implementation workspace.

Original Inbox assets should be treated as reproducible fixtures and should not be destructively modified in place unless explicitly authorized.

---

## 24. Hardware simulation/emulation instead of skipped coverage

If important physical hardware is unavailable, implementation/evaluation should use suitable simulation/emulation rather than simply omit the test.

Examples include:

- robots/embodied agents simulated in Unity, Unreal Engine, or another suitable environment;
- simulated sensors/actuators;
- simulated smart-home devices;
- emulated devices where useful.

Prefer the real surrounding software stack plus simulated missing hardware when feasible.

If Home Assistant OS semantics matter, use a real HAOS instance and simulate the unavailable devices around it. On the Ubuntu implementation host, virtualization is the appropriate class of deployment; Home Assistant Container is a distinct installation type and should not be treated as equivalent for HAOS-specific validation.

Simulation limitations and remaining physical-validation gaps must be documented.

---

## 25. Research-selected public skills require implementation reevaluation

Public skills identified during Research for possible use by the future system are candidates, not approved dependencies.

Implementation must evaluate them against the actual architecture, security model, maintenance state, license, current requirements, and overlap with native project capabilities.

Implementation may adopt, modify, replace, or reject/retire them.

The resulting decision and rationale should become durable project knowledge.

---

## 26. Huawei P30 unattended implementation connection

During the implementation run, the Huawei P30 (`ELE-L29`) is expected to remain physically connected to the implementation laptop with ADB enabled.

The device is intentionally configured for autonomous test access:

- lockscreen friction is disabled;
- relevant ADB/security prompts that would otherwise require owner presence have been disabled for this dedicated test device;
- the display remains on while connected to power.

Codex/the implementation harness should therefore be able to automate installation, debugging, logging, screenshots/control, and repeatable device-level tests without routine owner intervention.

---

## 27. Reference workload restructuring

The AI VTuber / AI Performer is no longer a separate reference-workload family.

It becomes the fixed **Tier C direction of the Social Companion** workload.

Social Companion structure:

- Tier A: Bedside Companion;
- Tier B: broader serious Social Companion, detailed design open to research;
- Tier C: Embodied AI VTuber / AI Performer.

Tier C must support multiple independent named vision streams, including initially:

- desktop/screen;
- webcam view of the human/operator;
- mirror/self-view of the agent/avatar;
- future additional streams where useful.

Streams must be independently enableable/disableable and preserve source identity/provenance. They may use different sampling, preprocessing, privacy, routing, retention, and latency policies.

---

## 28. Reference workload Tier-A anchors

### Ambient Environment / Home-Automation Agent

Tier A fixed direction: **Greenhouse Agent**.

Where HAOS semantics are relevant, use a real HAOS software instance with simulated/emulated devices rather than faking the entire HAOS layer.

### Interactive Desktop / Computer Agent

Tier A fixed direction: **Application-Attached CoWork Agent**.

The intended pattern is a dedicated agent attached to one specific application/domain, combining native API/tool surfaces and visual/UI interaction where useful.

Tier B remains a broader cross-application serious work system.

Tier C remains an ambitious desktop-work system including multi-agent orchestration, background/parallel work, skill creation, interactive teaching, and learning/programming from demonstration.

---

## 29. Seventh reference workload fixed: Embodied Agent / Robotics

The seventh workload family is now accepted as **Embodied Agent / Robotics**.

Tier directions:

- Tier A: Game / Virtual-World Agent;
- Tier B: Simulated Robotics / Digital-Twin Agent;
- Tier C: Physical / Hardware-in-the-Loop Robotics Agent.

The workload adds a genuinely orthogonal architecture stress dimension around VLA/control, sensor fusion, continuous control, physical safety, simulation/emulation, and simulation-to-real behavior.

No physical robot is currently available. Missing hardware is not grounds to skip the workload; maximize simulation/HIL coverage and preserve explicit physical-validation gaps.

---

## 30. Project Docs mirror semantics

Project Docs are stable always-on mirrors/snapshots for ChatGPT Project context.

Once Research is active, the matching repository files are the canonical evolving versions.

Project Docs should be deliberately refreshed when a material stable update needs to remain always-on context.

Do not allow Project Docs and repository files to evolve as two independent competing authorities.

---

## 31. Provider Capacity Snapshot wording refinement

Future-facing Provider Capacity Snapshot requirements should describe relevant plan/account limit dimensions without discussing saved/banked/bonus reset mechanisms.

The architecture/planning representation should simply model the provider capacity that is actually treated as available under the relevant plan/account snapshot.

Preparation history may retain the rationale, but final Research documents should avoid unnecessary discussion of non-modeled bonus mechanisms.



---

## 32. Task-specialized learned components, Teacher Workflows, and canonical data

The Research program must investigate when repeated narrow semantic/predictive functions are better served by task-specialized learned components than by recurring general-purpose model calls.

This is a supporting architecture capability, not a new primary focus.

Potential implementations include classical ML, embedding-plus-head systems, compact encoders, token classifiers, adapters, or other small learned mechanisms. The correct model class must be determined empirically.

Training/adaptation pipelines should support optional Teacher Workflows with zero, one, or multiple teachers. Teachers may include general/reasoning models, task/domain-specific or roleplay/social fine-tunes, multimodal/speech models, deterministic evaluators, runtime outcomes, and human/operator judgments.

A model may contribute a self-judgment only as one explicitly identified signal, preferably with isolated context; it must not become sole ground truth merely by judging its own output.

Reusable evidence should be captured once in a canonical representation and projected deterministically/versionedly into task/model-specific training formats when needed.

Research specifies approaches, contracts, data/evaluation design, and deferred experiments. It must not train/fine-tune deliverable project classifiers/models. Actual training, fine-tuning, quantization, shadow evaluation, promotion, and rollback happen during Implementation, potentially as opportunistic/preemptible background work when compute is otherwise idle.

Research should cover relevant concepts such as weak supervision, active learning, calibration/abstention, OOD/drift, continual/online learning, very-low-rank or other parameter-efficient adaptation, fast/slow adaptation and consolidation, replay/rehearsal, anti-forgetting, delayed feedback, and evaluation-gated promotion/rollback.

---

## 33. Social Companion affect, speech, and embodiment specialization

Across the three Social Companion tiers, human speech streams may independently enable transcript/text affect classification, audio/prosodic affect classification, or shared/multimodal fusion. Not every ASR/speaker stream must run every classifier.

The AI character may have a separate context-aware affect classifier that can use generated text plus compact dialogue/social/runtime state rather than only the literal spoken text. A capable general model may initially perform this function while real usage produces curated evidence; a smaller specialist may later take routine cases when implementation-time evaluation demonstrates adequacy.

Affect may feed both affect-dependent avatar micro-behavior and speech rendering so tone remains consistent. It is not a universal action gateway: unrelated or complex avatar actions may flow directly from LLM tool calls, VLA/controller paths, or other suitable capabilities.

Expressive TTS is required for Social Companion speech. The generic contract must not depend on inline tags alone and may support structured parameters, instructions, tags, control tokens, reference/style representations, and nonverbal vocalizations such as laughter, sighs, or throat-clearing according to provider capability.

Lip sync should be derivable from TTS audio and/or timing/phoneme/viseme data. Facial expression will commonly map to standard/custom blendshapes behind an abstract avatar-control contract.

Where VLA-style control is justified, a higher-level LLM/cognition layer may provide intent while the VLA/controller remains able to react locally to immediate obstacles/safety conditions without waiting for another high-level command.

---

## 34. Scoped manual routing and resource overrides

Model/provider routing, module routing, and hardware/resource allocation must support manual overrides without breaking or globally disabling automatic routing.

Useful semantics to research include force/pin, prefer, deny/exclude, scoped lifetime, and explicit reset/expiry.

Automatic routing/allocation should continue inside the remaining unconstrained decision space.

Manual overrides remain subject to capability compatibility and higher-authority security/privacy/safety policy.

---

## 35. Heterogeneous inference profiles and clustered hardware validation

Model suitability must be measured against explicit hardware/runtime profiles rather than a simplistic CPU-only Boolean.

Research/Implementation should consider CPU, GPU, NPU, and mixed execution with hardware architecture, memory subsystem, runtime/backend, quantization, concurrency/batching, latency, throughput, transfer cost, and residency where relevant.

The dedicated laptop remains the primary implementation host. Real NPU tests may require temporary use of the main PC or NUC; AMD-GPU tests may use the NUC; dual-GPU tests may use the main PC.

Prepare tests on the laptop when practical and group hardware-specific validation into one or a few coherent campaigns per alternate machine rather than repeatedly switching hosts for isolated checks.

---

## 36. Provider-output reuse governance for training/adaptation

Provider/source modules should expose known training/derivative-use restrictions in machine-readable form where practical.

Explicitly prohibited uses are hard blocks.

If a provider/model/source has no defined policy for a contemplated reuse, or applicability remains genuinely unclear, the default state is `unclear`: do not include it automatically, but permit explicit owner opt-in after a clear warning that the decision is taken at the owner's risk, and record the override.

This permits narrow task-specific training where not prohibited without pretending that an exhaustive positive allowlist exists.

Direct model distillation or other explicitly prohibited uses remain prohibited.

---

## 37. TypeSafe Jev as an approved project-test resource

TypeSafe Jev may be used by the system/project-under-test for evaluation, semantic decision experiments, routing/classification research, feature extraction, dataset/evidence workflows, or other suitable project purposes.

Current observed owner-account state during preparation:

- $5 `Monthly credit`;
- no payment information configured.

This credit is opportunistic/current state, not durable architectural capacity.

Jev is **not currently approved as a hidden Codex/Astra implementation copilot or general harness utility**, and no production-agent dependency on Jev is planned.

Dynamic provider information such as pricing, limits, credits, and terms normally needs refreshing no more than once per 24 hours unless an error/change signal or explicit owner request justifies an earlier refresh.

---

## 38. Contemporary learned-system prior-art leads

Research should investigate current work around:

- typed local semantic decision systems;
- learned routing with confidence/abstention/escalation;
- fast/slow continual adaptation and consolidation;
- feedback-driven retrieval/ranking;
- branchable/rollbackable experimental state;
- evaluation-gated self-improvement;
- durable long-running agent loops;
- capability-governed execution;
- portable model/adapter/evidence artifacts;
- specialist/MoE extraction and fallback;
- useful-work/effective-cost evaluation;
- multimodal sensor evidence with provenance.

Current preparation research found the RuVector/ruvnet ecosystem particularly rich in examples across these themes (including RuVector/OpenJev-style typed decisions, SONA, MetaHarness/Tiny Dancer, Ruflo, AgentDB/AgenticOW, Autogenous/Dream Machine/openAVO/rGi, RVM/RVF, MoE Foundry, APx, RuField/WorldGraph).

These are research leads/prior art only. Claims, benchmarks, and architectural choices require independent verification; predominantly first-party project code remains the intended direction.

---

## 39. Official GitHub integration for private repositories

The official GitHub plugin/integration is now considered a legitimate Implementation Harness option for working with private repositories and repo-native workflows.

The Harness Setup run may use/evaluate it for repository access, issues, pull requests, commits, review state, and related engineering-control-plane work, reducing the need for manual credential handling where the official integration is sufficient.

This does not by itself change the separate current restriction on using GitHub Actions as Implementation compute.

---

## 40. Preparation-only publication note — do not propagate

Current owner publication intent is preparation-only context and must not be injected into Research, Implementation Harness Setup, Implementation, or Architecture Review requirements.

If the owner later publishes parts of the system, the likely scope is:

- core;
- a small selected subset of reference workloads;
- template/reference modules.

Model weights should not be bundled regardless of model license; downstream users should obtain models themselves, with recommendations and original-source links where useful.

The owner controls publication manually. This note is intentionally excluded from the modular future-facing requirements set.


---

## 41. Client/frontend independence

Reference workloads and deployment profiles may use entirely different frontend technologies, languages, rendering stacks, and frameworks.

The platform must not impose one universal frontend implementation merely for consistency.

Clients should integrate through stable backend/platform contracts.

Where useful, session/identity/memory state should survive transitions between clients, including moving from a non-VR interface into a VR client during active use.

---

## 42. Social Companion Tier B standalone VR

Social Companion Tier B must support optional VR directly on a Quest-class standalone headset and remain fully useful without VR.

This is **not PCVR**.

The VR client runs on the headset while backend cognition/services may run on:

- a PC/server on the same LAN;
- a remote server;
- another suitable backend deployment.

The user should be able to put on the headset during an existing interaction and continue the same companion/session.

VR may add spatial/embodied capabilities beyond the non-VR frontend.

The implementation is not tied to one game engine. Unity or Unreal may be selected per reference implementation/experiment, and using both for different experiments is acceptable when useful.

---

## 43. Current engine baseline

The dedicated implementation laptop currently has:

- Unity 6.3 LTS (`6000.3.x`);
- Unreal Engine 5.8.4.

Both may be used for VR, game/virtual-world, robot simulation, digital twins, or other suitable implementation/evaluation work.

Do not impose one global engine choice when different engines are better suited to different tasks.

---

## 44. Home Assistant OS fixture

The owner has downloaded:

`haos_ova-18.3.qcow2.xz`

This Home Assistant OS KVM image archive will be placed into the owner-provided implementation workspace input/Inbox area before relevant work.

When HAOS-specific behavior matters, use the real HAOS VM and simulate unavailable devices around it rather than substituting Home Assistant Container or a fake HA layer.

---

## 45. Smartphone-local inference test path

For Persistent Personal Assistant Tier A and other mobile deployment testing, the Huawei P30 may be used to validate a fully local small-LLM path if technically feasible.

A candidate example is a Gemma4 E2B-class model through LiteRT-LM or a comparable mobile inference stack.

This is only a deployment-path test on constrained hardware, not a requirement that production use the P30 locally. External or LAN-hosted inference remains a normal/likely profile.

---

## 46. Quest / engine flexibility across VR reference work

Standalone Quest VR clients may be implemented using Unity, Unreal Engine, or another technically suitable stack.

Different VR experiments/reference implementations may intentionally use different engines.

Engine choice is a workload/implementation decision, not a universal platform contract.
