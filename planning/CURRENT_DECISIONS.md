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

- keep the setup/design work in the GPT-5.6 Sol Pro WebUI preparation workflow;
- optimize **Claude Code**, which is now the required implementation harness;
- research the current Claude Code version/install/authentication/model options immediately before implementation;
- design Claude Code skills/plugins, MCPs, hooks, native subagents, model allocation, context/project-memory strategy, Git workflow, permissions/security, issue workflow, and reproducible setup;
- target the actual dedicated implementation host.

Claude Code is fixed unless the owner explicitly changes this decision later; the setup run no longer compares Codex/Hermes/etc. as replacement primary harnesses.

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

Do not tell the research/review model that it is GPT-5.6 Sol Pro. Address it directly by role/instruction. Target-model names are allowed when they are technically relevant to a handoff/setup task.

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

All GPT-5.6 Sol Pro-style research, architecture, setup-design, and architecture-review runs occur in ChatGPT WebUI.

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

The former Codex permission configuration is historical only. Claude Code permissions/sandboxing must be designed independently during the setup run for high autonomy on the dedicated host.

### Existing local development/runtime software

Installed baseline includes:

- Claude Code (required implementation harness; installation/version/authentication finalized during setup);
- Unsloth Studio (currently preferred for supported purely local model workflows);
- Ollama;
- llama.cpp;
- Blender 5.2.2 + MCP;
- Unity 6.3 LTS (`6000.3.x`) + CLI + MCP;
- Unreal Engine 5.8.4 + MCP;
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

## 7. Claude Code is the required implementation harness

The owner has removed Codex from this implementation because Codex usage is already required by too many other projects and its subscription limits would not support this implementation reliably in parallel.

Current implementation decision:

- **Claude Code is the required primary implementation harness.**
- The specific Claude Code version/install channel/authentication path is selected during the later setup run.
- The specific Claude main model/configuration is intentionally not fixed this far in advance.
- The setup run optimizes Claude Code rather than comparing replacement primary harnesses.
- Codex may remain available for unrelated owner projects but must not be consumed by this implementation.

The setup run may add supported Claude Code skills/plugins, MCPs, hooks, native subagents, project memory/instruction files, code intelligence, Git tooling, or wrappers when useful.

All preparation/research/setup-design/architecture-review work remains in the GPT-5.6 Sol Pro WebUI workflow; the Claude Code switch applies to the actual implementation phase.

---

## 8. Claude Code main-agent and subagent model selection

The later GPT-6-Pro Implementation Harness Setup run must research the current Claude Code model landscape and the owner's actual Claude subscription entitlements immediately before implementation.

Current owner constraints:

- Claude Pro is the expected implementation subscription;
- Fable models are excluded because they require separate usage credits on Pro;
- do not enable/buy Fable credits for this project unless the owner explicitly changes that decision;
- the practical included model pool is expected to be Opus/Sonnet/Haiku families, subject to setup-time verification.

Do not hardcode one Claude model now.

Model/subagent selection must account for **effective total cost**, not simply nominal model tier.

Relevant cost factors include:

- Claude subscription allowance consumption;
- rolling/weekly/monthly usage pressure where applicable;
- wall-clock time;
- failure/rework probability;
- context loss/compaction overhead;
- subagent/orchestration overhead;
- opportunity cost.

A stronger Claude model may be more efficient end-to-end when it avoids corrective loops; a cheaper/faster model may be preferable for routine or mechanical roles.

### Implementation workforce

Primary workforce:

- Claude Code main agent;
- Claude Code native Claude subagents.

**Single external exception:**

- one bounded OpenCode auxiliary-subagent path may be used to save Claude usage when a suitable genuinely free/no-cost OpenCode model is available.

Current candidate is `glm-5.3-flash-free`, but free availability is explicitly temporary/dynamic and must be reverified during setup.

The OpenCode exception must:

- never silently use paid OpenCode models/balance;
- be benchmarked/smoke-tested for assigned task classes;
- test image-input support end-to-end before visual-task routing;
- remain subordinate to Claude Code orchestration/acceptance;
- fall inactive rather than spend money if the useful free model disappears.

All other local/external inference resources remain project-under-test resources only and must not secretly augment implementation reasoning.

---

## 9. Provider separation during Claude Code implementation

Claude Code subscription/OAuth is implementation-harness authentication, not a credential surface for the system-under-test.

Do not expose/reuse Claude Code's subscription OAuth as a production/test provider credential for the project runtime. A future Anthropic API/provider integration would require a separately approved supported API/cloud path and owner approval.

ChatGPT subscription/OAuth and GPT-5.6 Luna are currently **removed** from project-test resources to avoid consuming quota needed by unrelated Codex projects.

Codex / `codex exec` is likewise not an implementation or project-test resource for this run.

The owner has approximately **$62 of OpenAI API balance** available separately from ChatGPT/Codex subscription usage.

That balance expires on **2026-11-21** and may be **fully consumed before expiry** when doing so produces useful project knowledge. Conserving the balance is not an objective.

GPT-4o should be prioritized as a time-limited Social-Companion RP/creativity/behavioral reference while API access remains available.

The owner considers the intended Social-Companion system non-competing with OpenAI's current offerings because no current OpenAI model cleanly serves the intended use case. This owner position is relevant context but does not by itself resolve the contractual/policy interpretation.

Therefore GPT-4o training/teacher reuse is currently classified as **unclear pending explicit terms/policy determination**, not automatically allowed and not automatically forbidden.

Capture now with full provenance and keep training reuse separable. A later explicit decision/permission review may reclassify eligible artifacts.

---

## 10. Approved project-test inference resources

Existing accounts/credentials may be used by the **system/project-under-test** for evaluations/tests/provider work:

- Ollama Cloud Free;
- Groq Free;
- OpenRouter Free;
- NVIDIA NIM free endpoints;
- TypeSafe Jev;
- local models/runtimes;
- OpenAI API using the owner's existing prepaid balance.

ChatGPT subscription/OAuth is currently excluded.

OpenCode is special: its approved free-model path may act as the single external **implementation auxiliary-subagent exception** described above; OpenCode models are not otherwise automatically preferred as project runtime providers.

For OpenRouter and other dynamic/free services:

- use explicit named models for reproducibility;
- recheck current free limits/availability before relying on them;
- do not assume paid fallback capacity.

For GPT-4o specifically:

- API availability is temporary/deprecated;
- use is primarily evaluation/reference, not training-data generation for non-OpenAI replacement models;
- preserve provider/model/snapshot/date/policy provenance.

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

Claude Code/the implementation harness should therefore be able to automate installation, debugging, logging, screenshots/control, and repeatable device-level tests without routine owner intervention.

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

Jev is **not currently approved as a hidden Claude Code implementation copilot or general harness utility**, and no production-agent dependency on Jev is planned.

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

## 39. GitHub integration split between preparation and Claude Code implementation

The GPT-5.6 Sol Pro WebUI preparation/setup/review runs may use the official OpenAI GitHub integration for private-repository access and repo-native workflows.

Anthropic also provides an official **Claude Code GitHub App / Claude Code GitHub Action**.

The Claude Code setup run should evaluate:

- local `git` / `gh` as the default implementation path;
- the official Claude Code GitHub App/Action for repo-native issue/PR automation;
- Claude-Code-compatible GitHub MCP/plugin options where useful.

The official Claude Code GitHub Action runs through GitHub Actions. Under the current project policy it must not become routine Implementation compute. Using it for repo-native automation requires explicit owner acceptance of the corresponding GitHub Actions usage.

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


---

## 47. Initial avatar test fixtures

The first concrete implementation test avatar will be **Test-chan**.

Known owner-provided properties:

- sourced from Booth.pm;
- CC0;
- includes VRM0.

The owner will provide Test-chan through the implementation workspace input/Inbox area.

A separate suitable **VRM1** avatar will also be sourced and provided before the relevant interoperability tests.

Test-chan is a test fixture, not the final project avatar and not an architecture dependency.

---

## 48. Huawei P30 detailed unattended-debug posture

The Huawei P30 (`ELE-L29`) is a dedicated implementation test device and is intentionally configured for unattended Claude Code/harness access.

Current device state includes:

- no SIM card;
- no stored Wi-Fi network;
- ADB enabled and permanently connected to the implementation laptop during relevant testing;
- lockscreen friction disabled;
- `Enable view attribute inspection` enabled;
- `Allow ADB debugging in charge only mode` enabled;
- `Show touches` enabled;
- `Show all ANRs` enabled;
- `Always prompt when connecting to USB` disabled;
- `Verify apps over USB` disabled;
- log buffer size set to `1 MB per log buffer`;
- display configured to remain on while connected to power;
- other owner-approved security friction removed where needed for unattended testing.

This is an intentionally permissive dedicated test-device posture, not a recommendation for production/end-user Android devices.

Because no Wi-Fi network is stored, network provisioning for a test must be performed deliberately rather than assumed.

---

## 49. Preparation-only Home Automation hardware shortlist

A dated shortlist of inexpensive Home Assistant / Greenhouse-Agent sensors and actuators is maintained at:

`planning/HOME_AUTOMATION_HARDWARE_CANDIDATES_2026-10-24.md`

This is **preparation-only purchasing research**.

It must not be propagated into Research/Implementation requirements or treated as available hardware until the owner explicitly purchases/receives an item and adds it to the implementation inventory/input state.

The shortlist currently prioritizes inexpensive Zigbee sensing, one general-purpose switched/power-metered actuator, optional ESPHome soil/light sensing, leak/contact sensors, and later irrigation control.


---

## 50. Non-obvious / outside-the-box research behavior

The Research/Architecture run must actively explore beyond obvious or conventional solution classes.

For materially important questions, it should consider:

- reframing the problem;
- alternative system/module boundaries;
- cross-domain analogies/transfers;
- second-order and coupled effects;
- inverted assumptions and counterfactuals;
- adversarial counterexamples;
- unconventional combinations of simpler mechanisms;
- capabilities/opportunities omitted by incumbent systems;
- possibilities introduced by emerging model classes, hardware, protocols, or execution strategies.

This is disciplined exploration, not novelty for novelty's sake.

Non-obvious ideas remain hypotheses/candidates until supported by evidence and must meet the same feasibility, compatibility, security, maintainability, and evaluation standards as conventional approaches.

The owner's speculation about the internal identity/lineage of the Research model is **not** a project requirement and should not be propagated into Research instructions. The desired behavior is specified directly without model-identity priming.


---

## 51. OpenCode auxiliary-subagent exception

OpenCode is the only currently approved non-Claude implementation-agent exception.

Purpose: save Claude Pro usage by offloading bounded work to a genuinely free OpenCode model.

Current candidate: `glm-5.3-flash-free`.

Because free OpenCode models are time-limited/dynamic, setup must verify model availability, cost, limits, privacy/retention, tool behavior, and task competence immediately before use.

GLM-5.3-Flash itself supports image input, but the specific OpenCode free endpoint/alias must be tested end-to-end before visual tasks are routed there.

No paid OpenCode fallback is authorized without explicit owner approval.

---

## 52. Claude Pro Fable exclusion

Claude Fable models are excluded from the implementation model pool under the current Claude Pro plan because they require separate usage credits.

Do not enable/purchase Fable usage credits for this project unless the owner explicitly changes the decision.

Use the included Claude model families available under the owner's plan, expected currently to be Opus/Sonnet/Haiku, subject to setup-time verification.

---

## 53. OpenAI API balance and GPT-4o reference capture

The owner currently has approximately $62 of OpenAI API balance, separate from ChatGPT/Codex subscription usage.

The balance expires on **2026-11-21** and may be fully spent before expiry when useful. Do not conserve expiring balance merely to minimize API spend.

GPT-4o remains available through the API only temporarily and is currently scheduled to shut down on **2027-01-14**.

Priority Social-Companion capture areas include:

- roleplay/social naturalness;
- creativity and spontaneity;
- character voice/personality consistency;
- conversational texture;
- emotional/social reactions;
- multi-turn relationship dynamics;
- difficult comparison cases where GPT-4o materially differs from newer work-oriented models;
- evaluation prompts and human-reviewed qualitative references.

The goal is not to reproduce GPT-4o as a whole. The desired future system should combine useful traits from multiple sources and exceed the limitations of any individual teacher/reference.

### Training-reuse status

The owner considers the contemplated Social-Companion system non-competing with OpenAI's current products/services, but the exact applicability of OpenAI's current and upcoming model-training restrictions is a legal/policy interpretation that is not conclusively resolved in preparation.

Therefore:

- capture useful GPT-4o reference material before the balance/API window disappears;
- preserve exact model/snapshot/date/prompt/provenance;
- set `training_reuse_status: unclear_pending_terms_review`;
- keep evaluation/reference use separate from training-dataset pipelines;
- do not silently promote GPT-4o outputs/rankings/labels/rubrics into training signals;
- revisit applicable OpenAI terms/policies before any actual training reuse;
- record any later owner/legal/provider clarification or explicit override.

The existing project rule for unclear provider-output reuse remains applicable.

---

## 54. Codex as a Coding-Agent reference candidate

Codex is no longer part of this project's implementation workforce, but it remains a strong **external reference / benchmark / provider candidate** for Coding-Agent reference workloads.

Reasons include:

- it is purpose-built for software engineering;
- it supports ChatGPT-subscription authentication;
- it is available through CLI, IDE, web, and cloud workflows;
- higher-tier subscriptions provide materially higher coding-agent usage.

Research may compare the project's Coding-Agent reference systems against Codex or integrate a subscription-backed Codex path when that yields useful architecture/evaluation evidence.

This is not a requirement that Coding-Agent workloads depend on Codex, and any future subscription/usage budget should be evaluated separately from the Claude Code implementation budget.
