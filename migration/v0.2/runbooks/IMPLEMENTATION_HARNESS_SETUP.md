# Implementation Harness Research & Setup Runbook

**Status:** modular v0.2 preparation draft  
**Scope:** separate setup/design run immediately before implementation. It receives completed research/handoff material and optimizes the implementation environment. It does **not** redesign the cognitive platform.

---

## Purpose and Scope

Design and optimize the implementation environment for **Claude Code**, which is now the required implementation harness for this project.

The Implementation Harness Setup run is still a preparation/design run conducted separately before implementation.

Claude Code is a fixed owner decision for the implementation phase unless the owner explicitly changes it later.

Do **not** replace Claude Code with Codex, Hermes-Agent, or another primary implementation harness merely because another option benchmarks well. The setup task is to make Claude Code as effective, autonomous, reproducible, and usage-efficient as practical for this project.

The setup run should determine the current best-supported Claude Code configuration at that time, including:

- installation/update channel and version pinning strategy;
- Claude subscription/OAuth authentication path;
- main-model selection;
- native Claude Code subagent roles/model choices;
- permissions/sandboxing/approval behavior;
- project memory/instruction strategy;
- skills/plugins;
- MCP servers;
- hooks;
- code intelligence/LSP where useful;
- Git/GitHub workflow;
- context/compaction/resume strategy;
- observability/recovery;
- usage-budget strategy.

Use officially supported Claude Code/Claude subscription mechanisms. Do not switch the implementation workforce to metered Anthropic API billing or another paid inference path without explicit owner approval.

## Setup-Design Execution Surface

Conduct this setup/design run in ChatGPT WebUI.

For scripts, config generation, parsing, lightweight experiments, and setup-analysis code:

1. use the available OpenAI local/container execution environment first;
2. use GitHub Actions only when the local environment is insufficient or real CI/matrix behavior is materially required;
3. do not depend on ChatGPT Apps as a required execution surface.

This WebUI setup-design compute policy is separate from the later implementation run, which executes on the dedicated local host and must not use GitHub Actions as its own execution resource.

---

## Inputs

The setup run should receive:

- curated implementation handoff;
- authoritative requirements;
- architecture/specifications;
- implementation roadmap/dependency map;
- evaluation requirements;
- security/versioning/module standards;
- implementation host profile;
- owner-approved provider/tool constraints;
- relevant open implementation questions.

Deep research remains available on demand but should not be loaded wholesale when unnecessary.

---

## Claude Code Baseline and Optimization Scope

### Required harness

Claude Code is the required implementation harness.

The setup run must verify the **current** Claude Code release, official installation path, authentication options, model availability, usage semantics, and relevant features immediately before implementation rather than relying on stale preparation-time assumptions.

Pin or hold a specific Claude Code version only when reproducibility or a known regression makes that materially useful.

### Subscription authentication

Prefer the owner's Claude subscription through Claude Code's officially supported OAuth/native login path.

Do not silently fall back to Anthropic Console/API billing for the implementation agent.

If the owner's current Claude plan, model access, or usage limits are insufficient, surface that as a setup constraint and optimize within the available subscription before proposing any paid API dependency.

Current owner constraint:

- Claude Pro is the expected subscription tier for implementation;
- Fable models are not part of the allowed implementation pool because they require separate usage credits on Pro;
- do not enable/purchase Fable usage credits for this project unless the owner explicitly changes that decision;
- the practical included Claude pool should therefore be selected from the owner's then-current non-credit models (currently expected to be Opus/Sonnet/Haiku families), and must be reverified during setup.

### Optimization dimensions

The setup run should optimize Claude Code across dimensions including:

- long-horizon autonomy;
- context management and compaction behavior;
- session continuation/resume;
- filesystem/shell/local hardware access;
- native subagents;
- skills/plugins;
- MCP;
- hooks;
- project memory/instruction files such as `CLAUDE.md` where appropriate;
- code intelligence/LSP;
- Git/GitHub workflow;
- permission/security ergonomics;
- stability/recovery;
- subscription-usage efficiency;
- reproducibility;
- observability.

A wrapper/helper layer around Claude Code is allowed when it materially improves the workflow, but Claude Code remains the primary implementation agent.

## Implementation Host Profile

Dedicated implementation laptop:

- Ubuntu 26.04.1 LTS, fresh installation, dual boot;
- Intel Core i9-9980HK, 8C/16T;
- Turbo Boost disabled;
- 32 GB RAM;
- NVIDIA RTX 2070 8 GB;
- roughly 6–6.5 GB VRAM available in a lightweight/headless-ish environment;
- machine is dedicated to the implementation run so the owner's main workstation remains available.

The Huawei P30 (`ELE-L29`) used by mobile/Bedside reference testing will remain physically connected to this laptop with ADB enabled throughout implementation/testing.

It is intentionally configured for unattended automation:

- no SIM card is installed;
- no Wi-Fi network is currently stored on the device;
- lockscreen friction is disabled;
- `Enable view attribute inspection` is enabled;
- `Allow ADB debugging in charge only mode` is enabled;
- `Show touches` is enabled;
- `Show all ANRs` is enabled;
- `Always prompt when connecting to USB` is disabled;
- `Verify apps over USB` is disabled;
- Android log buffer size is set to `1 MB per log buffer`;
- relevant ADB/security prompts or barriers that would require owner presence have been disabled where the owner considers that acceptable for this dedicated test device;
- the display remains on while the device is connected to power;
- installation, debugging, logs, view-hierarchy inspection, UI automation, screenshots/control, ANR diagnosis, and repeatable device-level tests should be automatable without requiring the owner to unlock/confirm routine steps.

Because no trusted Wi-Fi network is preconfigured, network access should be provisioned deliberately by the implementation workflow when a test requires it rather than assumed to exist.

Treat this as an owner-authorized dedicated test-device posture, not a general recommendation for production user devices.

The previous Codex-specific security/approval configuration is historical and is **not** a Claude Code configuration baseline.

The Claude Code setup run must design an appropriate permission/security posture for this dedicated host. It should balance high autonomy against protection of the host, repository, credentials, owner-provided fixtures, connected devices, and external services.

Use current Claude Code permission/sandbox/hook mechanisms where useful. Do not enable unrestricted permission bypass merely by analogy with the former Codex configuration; justify any reduced-friction mode against the dedicated-host threat model.

The implementation run must execute its own code/tests/evaluations on the dedicated host or approved project providers.

**Do not use GitHub Actions as an execution resource for the implementation run.** GitHub Actions capacity is reserved for the separate WebUI research/setup-design/review runs unless the owner explicitly changes this constraint.

The implementation run may author CI/workflow files for the project when the architecture calls for them, but should not trigger/consume GitHub Actions minutes as part of its own implementation workflow under the current constraint.

---

## Owner-Provided Implementation Inbox

The implementation workspace may contain a dedicated owner-provided **Inbox** directory for fixtures/assets that should be consumed by the project but are not implementation-agent tools or subagents.

Known planned avatar fixtures include:

- **Test-chan** as the first concrete test avatar:
  - CC0;
  - sourced by the owner from Booth.pm;
  - includes VRM0;
- an additional suitable VRM1 avatar to be supplied by the owner before the relevant interoperability tests;
- a matching cross-format avatar fixture available in:
  - VRM;
  - VRChat-ready Unity package (`.unitypackage`);
  - PMX/MMD format;
  - associated textures/assets.

The owner has also downloaded the Home Assistant OS KVM image archive:

- `haos_ova-18.3.qcow2.xz`

and plans to place it in the same owner-provided workspace input area before relevant implementation/testing begins.

Treat these as real interoperability/test fixtures. Verify fixture presence/version before use rather than assuming a path forever.

Do not modify or discard original Inbox assets in place unless explicitly authorized. Prefer copying/deriving working assets into project-controlled locations so the original fixture remains reproducible.

The Inbox mechanism should be generic enough for future owner-provided test assets/fixtures without becoming a hidden dependency on undocumented local files.

---

## Existing Host Software Baseline

Already installed/available:

### AI/model/runtime

- Claude Code — required implementation harness; installation/version/authentication must be verified/finalized during the setup run;
- Unsloth Studio — currently preferred for supported purely local model workflows;
- Ollama;
- llama.cpp.

Codex may exist on owner machines for unrelated projects, but this implementation must not consume Codex as its main agent, subagent, helper, judge, or test-intelligence path.

### 3D / game / interactive

- Blender 5.2.2 + MCP;
- Unity 6.3 LTS (`6000.3.x`) + CLI + MCP;
- Unreal Engine 5.8.4 + MCP.

A Meta Quest 3 is a target device for the standalone Social-Companion VR client.

Unity and Unreal are both valid for VR, virtual-world, robotics-simulation, or other engine-backed experiments. Select the engine per task based on technical fit; the project does not impose one global engine. Different reference implementations/experiments may intentionally use different engines when doing so yields useful evidence.

### Development

- `uv` + system Python;
- `nvm` + system Node;
- `gvm` for Go;
- `javm` for Java;
- `rustup` for Rust;
- Android SDK + emulator + documentation;
- GCC / Clang / standard toolchains;
- development and Ubuntu Server metapackages;
- Docker suite without Docker Desktop.

### Other

- Steam + Proton;
- `yt-dlp`;
- TwitchDownloaderCLI;
- Obsidian.

Treat this as **available baseline capability**, not a closed set.

You may install additional software when justified.

Prefer native Linux where practical, but containers, Wine/Proton, or other compatibility approaches are permitted.

Free non-OSI/source-available software may be considered, especially as an alternative, when licensing/telemetry/privacy/redistribution constraints are documented.

---

## Experimental / Preview Features

Current Claude Code experimental/preview features may be evaluated when they materially improve this project's implementation workflow.

They are not mandatory.

Use them only when their expected value outweighs stability/reproducibility risk, and document any version dependency or fallback.

Do not make a preview capability a hard project dependency merely because it exists.

---

## Tooling Freedom

You may investigate/use suitable:

- Claude Code plugins;
- Claude Code skills;
- third-party skills;
- public skill registries such as `skills.sh`;
- MCP servers;
- Claude Code hooks;
- native Claude Code subagents;
- project memory/instruction mechanisms such as `CLAUDE.md`;
- LSP/code-intelligence integrations;
- local CLI tools;
- code intelligence;
- debuggers;
- profilers;
- linters/formatters;
- test systems;
- local search/indexing;
- graph tools;
- documentation tools;
- repo-analysis tools;
- context-management helpers;
- planning systems;
- custom local extensions;
- issue/work tracking integrations.

The GPT-6-Pro/WebUI setup or review runs may use the available OpenAI GitHub integration for repo-native preparation/review work.

Claude Code also has an official Anthropic GitHub App / `anthropics/claude-code-action` integration. The setup run should evaluate it alongside local `git`/`gh` and any useful Claude-Code-compatible GitHub MCP/plugin path.

Important: the official Claude Code GitHub Action executes through GitHub Actions. Under the current project policy it must **not** become routine implementation compute. It may be installed/configured for repo-native PR/issue automation only if the owner explicitly accepts the corresponding GitHub Actions usage for that workflow.

Local Claude Code + `git`/`gh` remains the default implementation path.

Local tooling is preferred where capability/reliability are competitive.

The final recommended implementation-harness equipment should not introduce new credential-bearing or paid service dependencies without owner approval.

Existing owner-approved project-test provider credentials are governed separately and must not be repurposed as implementation-agent workforce.

---

## Third-Party Software Policy

OSI-approved open-source software is preferred when technically competitive.

Free non-OSI, source-available, or otherwise freely usable software may also be considered, particularly as an alternative solution.

For nontrivial third-party software, document relevant:

- licensing/usage restrictions;
- redistribution constraints;
- telemetry/privacy implications;
- maintenance/lock-in risk;
- Ubuntu/Linux compatibility;
- operational/security implications.

Do not reject a technically strong tool solely because it is non-OSI when its terms are acceptable for the project's use, but do not hide restrictions behind "free".

---

## Skills, Plugins, and MCPs

Search public skill/plugin/MCP ecosystems when useful for optimizing implementation.

Candidate components must be evaluated for:

- actual project relevance;
- permissions;
- security;
- maintenance;
- license;
- compatibility;
- prompt/context behavior;
- stability;
- host compatibility;
- credential requirements;
- duplicate functionality.

Do not install large collections merely for optionality.

Prefer a small deliberate tool surface.

---

## Research-Selected System Skill Candidates

Public skills/components identified during Research for possible use by the future system are **candidates, not approved dependencies**.

During implementation, evaluate each candidate against:

- actual architecture/contracts;
- security/permissions;
- code quality;
- maintenance status;
- license;
- portability;
- current requirements;
- overlap with native project capabilities.

Implementation may:

- adopt;
- modify/fork where legally/technically appropriate;
- replace;
- or retire/reject

a Research-selected candidate.

Persist the decision/rationale so Research recommendations do not become cargo-cult dependencies.

---

## Custom Tooling

If a meaningful harness capability is missing, you may design/build a small custom tool, skill, MCP server, plugin, helper, or integration.

Custom additions must be:

- documented;
- version-controlled;
- testable;
- reproducible;
- appropriately licensed;
- narrow enough to maintain.

Do not invent custom tooling when a superior maintained solution already exists.

---

## Main-Agent Configuration

The main implementation agent runs in Claude Code.

Do not permanently hardcode one Claude model in preparation artifacts because Claude Code model availability and plan entitlements can change.

The setup run must determine the best current main-agent model/configuration for long-horizon implementation using:

- current official Claude Code/model guidance;
- the owner's actual Claude subscription/entitlements at setup time;
- trustworthy current operational evidence;
- project/task characteristics;
- limited representative validation where uncertainty is material.

Prefer a configuration that minimizes **effective end-to-end implementation cost**, including subscription consumption, failure/rework probability, latency, context loss, and orchestration overhead.

A stronger model may be cheaper overall when it avoids repeated corrective loops; a cheaper/faster model may be better for routine or mechanical work.

Do not brute-force every available Claude model × configuration permutation merely because it can be measured.

---

## Subagents

Use Claude Code's native subagent/delegation mechanisms when they materially improve quality, throughput, context isolation, or separation of concerns.

Subagents may use different Claude models/configurations when supported and useful.

For every proposed role determine:

- task class;
- Claude model/configuration;
- permissions;
- tools/skills;
- context scope;
- expected output;
- escalation behavior;
- termination behavior;
- expected subscription/effective cost;
- evaluation basis.

### Effective-cost rule

Do not assume the smallest/weaker Claude model is automatically the cheapest useful choice.

Consider:

- Claude subscription allowance consumption;
- scarce rolling/weekly/monthly usage pressure where applicable;
- wall-clock time;
- latency;
- failure probability;
- expected rework;
- context/orchestration overhead;
- opportunity cost.

Use the least expensive configuration that **reliably** clears the required quality threshold.

### Evidence-first selection

Do not exhaustively benchmark every model/configuration.

Prefer:

- current official information;
- trustworthy current community/operational evidence;
- existing relevant evaluations;
- model/task fit;
- targeted validation only where the uncertainty materially affects the implementation setup.

---

## Implementation-Workforce Boundary

The primary implementation workforce is:

1. Claude Code main agent;
2. Claude Code native Claude subagents;
3. **one explicit external exception: an OpenCode instance used as a bounded auxiliary subagent.**

All other local models and external APIs remain project-under-test resources only and must not become hidden implementation copilots, planners, judges, or reviewers.

### OpenCode exception

OpenCode is the **only** currently approved non-Claude implementation-agent exception.

Its purpose is to reduce Claude subscription pressure by offloading suitable bounded tasks when a genuinely free/no-cost model is available.

Current candidate:

- `glm-5.3-flash-free` through OpenCode, currently advertised as a limited-time free model.

Setup requirements:

- verify that the model/alias is still free immediately before use;
- verify actual rate/usage limits and availability;
- do **not** silently fall back to paid OpenCode models or paid balance;
- verify task competence before routing meaningful work;
- verify image-input support end-to-end before assigning visual tasks;
- keep Claude Code responsible for orchestration, integration, acceptance, and escalation;
- treat OpenCode output as untrusted implementation-subagent output that must pass normal tests/review;
- do not let the auxiliary instance mutate critical architecture or security policy without Claude Code validation.

Good candidate tasks may include:

- bounded visual/image-analysis tasks if direct image input works;
- mechanical code transformation;
- repository/file analysis;
- low-risk boilerplate;
- structured extraction;
- other clearly scoped work where quality is empirically adequate.

If the useful free model disappears or its limits become too restrictive, the OpenCode workforce exception may simply become inactive. Paid fallback requires explicit owner approval.

### Prohibited implementation-workforce resources

The following remain prohibited as hidden implementation workers unless the owner later changes policy:

- local Unsloth/Ollama/llama.cpp models;
- Ollama Cloud;
- Groq;
- OpenRouter outside the explicitly approved OpenCode auxiliary instance;
- NVIDIA NIM;
- TypeSafe Jev;
- ChatGPT/OpenAI models;
- Anthropic Console/API-key inference outside the approved Claude Code subscription workflow;
- other external inference APIs.

Those resources may still be used by the **system/project being implemented** for integration tests, evaluations, benchmark scenarios, runtime/provider experiments, Model Suitability work, or project-specific training/adaptation.

--- 

## Hardware Simulation / Emulation During Implementation

Do not skip an architecturally important hardware-dependent test merely because the physical device is unavailable.

Use an appropriate simulation/emulation environment when useful fidelity is achievable.

Examples include:

- robot/embodied-agent simulation in Unity 6.3 LTS, Unreal Engine 5.8.4, or a suitable robotics simulator;
- simulated sensors/actuators;
- emulated edge/mobile devices where the real device is unavailable;
- simulated smart-home devices attached to the real Home Assistant software stack.

Relevant simulator/plugins may be installed or provided by the owner when needed.

When Home Assistant OS behavior itself matters, use a real HAOS instance in a VM on the Ubuntu host and simulate/emulate the missing devices around it rather than replacing HAOS with a fake. Home Assistant Container is a different installation type and must not be treated as equivalent for HAOS-specific validation.

The owner-provided `haos_ova-18.3.qcow2.xz` KVM image archive should be used as the initial HAOS fixture when present, after normal integrity/version checks and extraction/provisioning.

Clearly document what the simulation validates and what still requires later physical-hardware testing.

---

## Project-Test Provider Boundaries

Existing owner-approved resources for **project-under-test** work may include:

- Ollama Cloud Free — already configured on the implementation host;
- Groq Free — account/key exists but integration may still need setup;
- OpenRouter Free — account/key exists but integration may still need setup;
- NVIDIA NIM free endpoints;
- TypeSafe Jev — owner account currently observed with a $5 `Monthly credit` balance and no payment information configured;
- local models/runtimes;
- OpenAI API using the owner's existing prepaid API balance (currently approximately $62, subject to recheck before use).

**ChatGPT subscription/OAuth is currently removed from project-test resources** to avoid interfering with unrelated Codex usage limits.

The Groq/OpenRouter accounts intentionally have no payment information configured; do not assume paid fallback capacity.

For OpenRouter:

- use explicit named models only;
- do not rely on a random/free router when reproducibility requires knowing the actual model;
- assume limits applicable to a fresh account that has not unlocked higher free limits through a credit purchase.

Provider limits must be checked/documented at the time of setup or evaluation rather than assumed static. Dynamic provider metadata such as pricing, limits, credits, and terms should normally be refreshed at most once per 24 hours; invalidate that cache earlier only when a provider/runtime error, explicit change signal, or owner request makes an earlier check useful.

Jev is currently approved as a **project-under-test inference/evaluation resource**, not as a hidden Claude Code implementation copilot or general harness utility, and no production dependency on Jev is assumed.

### OpenAI API project-test / GPT-4o reference rule

OpenAI API usage is separate from ChatGPT/Codex subscription usage and may use the owner's existing API balance when explicitly useful.

GPT-4o is a temporary Social-Companion **evaluation/reference** candidate while it remains available in the API.

Permitted planned use includes:

- RP/creativity comparison runs;
- qualitative behavioral reference;
- prompt-suite benchmarking;
- human-reviewed examples;
- identifying desirable interaction characteristics;
- comparing candidate Social-Companion systems against a 4o reference profile.

**Do not automatically place GPT-4o outputs, rankings, labels, rubrics, or other derived training signals into datasets for training a non-OpenAI Social-Companion model.**

OpenAI's current terms/policies restrict using outputs to develop competing/alternative models, with only narrow exceptions. Therefore mark GPT-4o-derived reference artifacts with provenance such as:

- `training_allowed: false`;
- provider/model/snapshot;
- generation date;
- intended use: evaluation/reference only;
- relevant policy/terms snapshot.

Recheck OpenAI terms and GPT-4o availability before any use. GPT-4o API snapshots are currently deprecated and scheduled for shutdown on **2027-01-14**.

Codex / `codex exec` and ChatGPT subscription models are intentionally excluded from this implementation workflow because their subscription usage is reserved for other owner projects.

---

## Local Model/Test Capability

The laptop can comfortably host lightweight models fitting within roughly 6 GB usable VRAM, including many embeddings/classifiers/small specialized models.

Larger quantized/offloaded models may be technically usable for slow background project evaluation through tools such as Unsloth Studio, Ollama, or llama.cpp.

For smartphone-local inference validation on the Huawei P30, a very small mobile LLM stack — for example a Gemma4 E2B-class model through LiteRT-LM or a comparable runtime/model if supported at implementation time — may be tested purely to validate the local deployment path. External/LAN inference remains the more realistic default candidate for that constrained device.

Do not confuse "technically runs eventually" with "appropriate interactive runtime".

Avoid implementation-agent workflows that waste hours polling long-running project-model tests when asynchronous/background execution and later result collection can be used.

---

## Project Model Training and Hardware Validation Campaigns

Project-specific classifier/model training, fine-tuning, adapter work, quantization, and promotion happen during Implementation when the relevant contracts, capture data, and evaluation gates are mature enough. Where practical, schedule such work as preemptible/background compute that uses otherwise idle resources and yields to foreground implementation/testing needs.

The dedicated laptop remains the primary implementation machine. Some real-hardware validation requires temporary execution elsewhere:

- NPU validation may use the owner-provided main PC or NUC because the laptop has no known NPU;
- AMD-GPU validation may use the NUC;
- dual-GPU validation may use the main PC.

Prepare as much implementation and automated testing as possible on the laptop first, then cluster device-specific physical-hardware tests into one or a small number of coherent campaigns per target machine instead of repeatedly switching hosts for isolated checks.

Record the exact hardware/runtime profile used for each result so Model Suitability evidence remains conditional and reproducible.

---

## Provider Capacity Snapshot During Setup

When provider capacity matters to implementation/evaluation planning, generate time-stamped capacity snapshots using only guaranteed/normal plan resources.

Capture relevant limit classes such as:

- RPM/TPM;
- daily quotas;
- concurrency;
- rolling windows;
- 5-hour windows;
- weekly/monthly limits;
- model/reasoning restrictions;
- context/input/output limits;
- free quota/credit state;
- reset semantics;
- checked-at timestamp/source.


---

## Model Suitability Guidance During Implementation

Use and extend the project's Model Suitability Knowledge Base.

When implementation/evaluation reveals useful evidence, record:

- adequate model class/size;
- when larger classes become necessary;
- tool-use/structured-output requirements;
- vision/audio/speech/modality requirements;
- context/streaming requirements;
- strong/weak/unsuitable families;
- feature-specific differences;
- quantization sensitivity;
- reasoning requirements;
- effective cost;
- CPU/GPU/NPU or mixed-execution profile where relevant;
- cold/warm latency, memory footprint, throughput, and backend/quantization details where relevant;
- calibration/abstention/OOD behavior for specialized learned components where relevant;
- evidence/confidence.

Do not bury reusable model-selection evidence in transient implementation logs.

---

## Issue and Work Tracking

Evaluate whether GitHub Issues or another lightweight repo-native system should act as a cross-run engineering control plane.

A useful workflow may support:

- architecture-review findings;
- implementation tasks;
- blockers;
- dependency relationships;
- acceptance criteria;
- links to requirements/ADRs;
- status/reverification.

Do not introduce issue ceremony when direct implementation is simpler.

The goal is cross-run continuity and traceability, not project-management theater.

---

## Setup Evaluation

Compare meaningful **Claude Code configurations and extensions** before finalizing. Claude Code itself is fixed; the setup experiment space is configuration, model allocation, native subagents, permissions, memory/instructions, skills/plugins, MCP, hooks, Git workflow, supporting local tooling, and the bounded OpenCode-free-model auxiliary-subagent exception.

Relevant measurements/evidence may include:

- implementation quality;
- context retention;
- speed;
- subscription/usage consumption;
- effective task cost;
- subagent overhead;
- error/rework rate;
- test success;
- code-review findings;
- unnecessary tool calls;
- autonomy duration;
- recovery after compaction/restart;
- reproducibility;
- host/resource utilization where relevant;
- security/approval ergonomics.

Avoid exhaustive permutation testing with poor expected information value.

---

## Reproducibility

The final setup should contain enough configuration/documentation to recreate the environment.

Where appropriate include:

- pinned versions;
- install/bootstrap instructions;
- configuration files;
- selected plugins/skills/MCPs;
- permission/approval configuration;
- environment checks;
- smoke tests;
- "doctor"-style validation if research shows it is worthwhile.

Do not rely on undocumented manual state.

---

## Setup Completion Output

Before implementation begins, produce/finalize:

- selected Claude Code version/install channel/authentication path;
- main-agent Claude model/configuration;
- Claude Code native subagent definitions if any;
- OpenCode auxiliary-subagent configuration/limits/capability tests if the exception is active;
- context-management configuration;
- security/approval model;
- installed/required local tooling;
- plugins/skills/MCPs;
- issue/work workflow if useful;
- project-test provider boundaries;
- reproducible bootstrap;
- smoke/health checks;
- implementation start instructions;
- links to authoritative handoff documents.

Then hand control to the implementation run.
