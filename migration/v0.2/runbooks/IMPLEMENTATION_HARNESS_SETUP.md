# Implementation Harness Research & Setup Runbook

**Status:** modular v0.2 preparation draft  
**Scope:** separate setup/design run immediately before implementation. It receives completed research/handoff material and optimizes the implementation environment. It does **not** redesign the cognitive platform.

---

## Purpose and Scope

Design the strongest practical implementation harness/environment for implementing the researched system.

Primary target implementation model:

- GPT-6 Astra.

Leading baseline harness:

- Codex CLI v0.153.4.

The baseline is a strong candidate, not an immutable requirement.

You may recommend an alternative harness (for example a suitable Hermes-Agent configuration) only when there is a clear evidence-based net benefit and the owner can still use the ChatGPT subscription through an officially supported OAuth path.

Replacing the known Codex baseline carries a high burden of proof.

Do not choose a different harness merely because it is novel.

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

## Harness Baseline and Alternatives

### Codex baseline

Known candidate:

- Codex CLI v0.153.4;
- GPT-6 Astra available;
- known required experimental context-management behavior works for the owner in this version.

Do not upgrade simply because a newer release exists.

Newer versions may be evaluated separately when evidence suggests material value.

Migration requires evidence that required behavior — particularly context management and project-specific workflows — remains equal or better.

### Alternative harness

An alternative is acceptable only when it demonstrably improves the implementation program on relevant dimensions such as:

- Astra support;
- ChatGPT-subscription OAuth support;
- long-running autonomy;
- context management;
- filesystem/shell/local hardware access;
- subagents;
- plugins/skills/MCPs;
- Git/GitHub workflow;
- stability/recovery;
- usage efficiency;
- reproducibility;
- observability;
- approval/security controls.

A hybrid arrangement may be considered when it is genuinely simpler or stronger than one harness alone.

---

## Implementation Host Profile

Dedicated implementation laptop:

- Ubuntu 26.04.1 LTS, fresh installation, dual boot;
- Intel Core i9-9980HK, 8C/16T;
- Turbo Boost disabled;
- 32 GB RAM;
- NVIDIA RTX 2070 8 GB;
- roughly 6–6.5 GB VRAM available in a lightweight/headless-ish environment;
- machine is dedicated to the implementation run so the owner's main workstation remains available.

Known Codex CUDA-capable security/approval baseline that has already worked:

- `sandbox_mode = danger-full-access`;
- `approval_policy = on-request`;
- `approvals_reviewer = guardian_subagent`.

This is an allowed known-good baseline, not automatically the final recommendation.

Ordinary implementation/test work should run locally on this host rather than consume GitHub Actions merely for compute.

---

## Existing Host Software Baseline

Already installed/available:

### AI/model/runtime

- Codex;
- Unsloth Studio — currently preferred for supported purely local model workflows;
- Ollama;
- llama.cpp.

### 3D / game / interactive

- Blender 5.2.2 + MCP;
- Unity 6.6 + CLI + MCP;
- Unreal Engine 5.8.2, linked into `~/.local/bin`, + MCP.

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

## Experimental Features

Experimental harness/Codex features are allowed.

They are not mandatory.

Experimental context management is explicitly within scope.

Use experimental features when evidence indicates meaningful value and their failure modes are acceptable.

Do not make an experimental capability a required dependency merely because it exists.

---

## Tooling Freedom

You may investigate/use suitable:

- Codex plugins;
- third-party skills;
- public skill registries such as `skills.sh`;
- MCP servers;
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

Local tooling is preferred where capability/reliability are competitive.

The final recommended implementation-harness equipment should not introduce new credential-bearing or paid service dependencies without owner approval.

Existing owner-approved project-test provider credentials are governed separately and must not be repurposed as implementation-agent workforce.

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

GPT-6 Astra is the primary implementation target model.

Astra Xhigh or Max are strong initial main-agent candidates for long-horizon implementation because greater reasoning may reduce expensive corrective loops.

This is a **working hypothesis**, not a guaranteed subscription-accounting rule.

Do not brute-force every Astra reasoning level across a large benchmark matrix.

Use:

- official model guidance;
- trustworthy community operational evidence;
- project/task characteristics;
- limited representative validation when uncertainty is material.

Select the configuration expected to minimize **effective end-to-end implementation cost**, not nominal reasoning level alone.

---

## Subagents

Specialized subagents may be defined when they materially improve quality, throughput, reliability, context management, or separation of concerns.

For every proposed role determine:

- task class;
- model;
- reasoning effort;
- permissions;
- tools;
- context scope;
- expected output;
- escalation behavior;
- termination behavior;
- expected effective cost;
- evaluation basis.

### Effective-cost rule

Do not assume the smallest/weaker model is automatically cheapest.

Consider:

- subscription allowance consumption;
- scarce rolling/weekly-window pressure;
- wall-clock time;
- latency;
- failure probability;
- expected rework;
- orchestration overhead;
- opportunity cost.

A configuration such as Luna Max may legitimately be more cost-effective than a nominally stronger/other-family Low configuration if plan accounting and reliability favor it.

Use the least expensive configuration that **reliably** clears the required quality threshold.

### Evidence-first selection

Do not benchmark every model × reasoning combination merely because it is theoretically measurable.

Prefer:

- official information;
- trustworthy public/community experience;
- existing evaluations;
- model/task fit;
- targeted validation only where the uncertainty materially affects the setup.

---

## Hard Subagent Boundary

**The implementation harness itself must not use local models or external APIs outside the approved ChatGPT-subscription/OAuth harness as its own subagents, copilots, hidden judges, planners, or reasoning helpers.**

This prohibition includes project-test resources such as:

- local Unsloth/Ollama/llama.cpp models;
- Ollama Cloud;
- Groq;
- OpenRouter;
- NVIDIA NIM;
- other external inference APIs.

Those resources exist only for the **system/project being implemented**, for example:

- module/provider integration tests;
- evaluations;
- test fixtures;
- runtime/provider experiments;
- capability validation;
- benchmark scenarios.

They must not augment the implementation agent's own reasoning workforce.

---

## Project-Test Provider Boundaries

Existing owner-approved resources for **project-under-test** work may include:

- Ollama Cloud Free;
- Groq Free;
- OpenRouter Free;
- NVIDIA NIM free endpoints;
- local models/runtimes;
- ChatGPT-subscription OAuth under the Luna-only rule below.

For OpenRouter:

- use explicit named models only;
- do not rely on a random/free router when reproducibility requires knowing the actual model;
- assume limits applicable to a fresh account that has not unlocked higher free limits through a credit purchase.

Provider limits must be checked/documented at the time of setup or evaluation rather than assumed static.

### ChatGPT OAuth project-test rule

If the project-under-test exercises a ChatGPT subscription/OAuth provider during the Astra implementation run:

- use **GPT-5.6 Luna only**;
- reasoning may be configured up to Max;
- never use GPT-6 Astra as the project's inference/judge/evaluation provider inside the Astra implementation run.

This prevents project testing from consuming the same scarce Astra capacity required to implement/fix the system.

If substantially stronger intelligence is genuinely required for a project evaluation, use an approved external test provider instead, subject to current availability/limits.

### `codex exec`

`codex exec` may be exposed as one optional **Test Intelligence Provider** for project evaluation.

It is not:

- a substitute for implementation subagents;
- a preferred provider merely because it is available;
- permission to use Astra recursively.

Model/provider selection for project tests remains part of the system's provider/evaluation architecture.

---

## Local Model/Test Capability

The laptop can comfortably host lightweight models fitting within roughly 6 GB usable VRAM, including many embeddings/classifiers/small specialized models.

Larger quantized/offloaded models may be technically usable for slow background project evaluation through tools such as Unsloth Studio, Ollama, or llama.cpp.

Do not confuse "technically runs eventually" with "appropriate interactive runtime".

Avoid implementation-agent workflows that waste hours polling long-running project-model tests when asynchronous/background execution and later result collection can be used.

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

Do **not** count saved/banked/bonus resets as dependable capacity.

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

Compare meaningful harness/setup alternatives before finalizing.

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

- selected harness and version;
- main-agent model/reasoning configuration;
- subagent definitions if any;
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
