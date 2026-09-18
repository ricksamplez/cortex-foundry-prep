# Research Completion & Implementation Handoff Requirements

**Status:** initial canonical research document — modular charter set v0.2 candidate  
**Scope:** defines when architecture research is sufficiently complete and what must be handed to the later implementation-harness setup and implementation phases.

---

## Research Is Not Complete at "Plausible Architecture"

The research phase is not complete merely because a coherent architecture diagram or plausible stack exists.

Completion requires enough evidence, specification, compatibility policy, evaluation design, and implementation planning for an independent implementation effort to proceed without reconstructing foundational decisions from chat history.

Remaining uncertainty is allowed, but it must be explicit, bounded, and non-contradictory with the implementation plan.

---

## Research Completion Criteria

Before the research phase is declared complete, the project should have:

1. a stable Requirements Charter;
2. a coherent and navigable research Vault;
3. a documented dependency-aware research map;
4. traceable evidence for important architectural claims;
5. a canonical extensible ontology;
6. a capability model;
7. a module/extension model;
8. a module documentation standard;
9. an architecture specification;
10. an execution/compute strategy;
11. routing/allocation/scheduling architecture;
12. module-level routing/workflow semantics;
13. state/context/memory architecture;
14. context/instruction-artifact handling strategy;
15. security and trust model;
16. observability and replay strategy;
17. controlled optimization/improvement strategy;
18. versioning and compatibility policy;
19. schema-evolution strategy;
20. module lifecycle policy;
21. deployment profiles;
22. reference-workload mappings for all required workload tiers;
23. evaluation framework;
24. documented experiments where needed to resolve important uncertainty;
25. major ADRs/decision records;
26. rejected-alternative records where valuable;
27. Model Suitability Knowledge Base structure and initial guidance sufficient for implementation;
28. provider/capacity representation required by the implementation/evaluation plan;
29. implementation dependency map;
30. implementation roadmap;
31. curated implementation-handoff package;
32. remaining uncertainty and open implementation questions explicitly identified;
33. no known major unresolved contradiction between requirements and architecture;
34. no known silent loss of required v0.1/post-v0.1 semantics from the modular requirements set;
35. system naming either deliberately resolved or explicitly deferred with rationale if architecture identity is still insufficient.

The research program may strengthen these criteria when evidence identifies a meaningful missing gate.

---

## Reference Workload Readiness

Research completion does not require all 21+ reference systems to be implemented.

It does require the reference systems to be specified well enough that:

- their required capabilities are understandable;
- architecture stress dimensions are known;
- acceptance/evaluation expectations are defined;
- missing core abstractions would be visible;
- planned implementation slices can choose representative workloads intentionally.

At least one realistic implementation path should exist from core/runtime work to useful vertical slices.

---

## Curated Implementation Handoff

The implementation target should receive a **curated implementation package**, not the entire raw history of the research program.

The current primary implementation target model is GPT-6 Astra. Handoff material should therefore be written so that Astra can implement efficiently, while the implementation-harness setup run remains free to select the best suitable harness/environment around that target.

The handoff should contain, at minimum:

- authoritative requirements;
- architecture;
- canonical terminology;
- core/module contracts;
- extension/contribution contracts;
- routing/workflow semantics;
- relevant ADRs;
- implementation dependency map;
- implementation roadmap;
- evaluation requirements;
- module standards;
- documentation standards;
- coding/quality standards that research has established;
- security rules;
- versioning/compatibility rules;
- relevant research references/evidence;
- Model Suitability guidance relevant to the implementation;
- open implementation questions;
- known deferred experiments;
- unavailable-hardware simulation/emulation plans and remaining physical-validation gaps;
- candidate public skills or reusable external components that implementation must evaluate before adoption;
- owner-provided implementation fixtures/assets expected at implementation time;
- assumptions that implementation must validate;
- pointers into deeper research where needed.

Research detail should remain accessible on demand through the Vault without being injected wholesale into every implementation context.

---

## Handoff Progressive Disclosure

The implementation package should distinguish:

### Always-relevant implementation authority

Small/high-value documents that the implementation harness should keep readily available.

### Task-/module-specific reference

Detailed specifications loaded only when implementing/reviewing affected subsystems.

### Deep research/evidence

Source material and synthesis available for disputes, design questions, or architecture changes.

### Historical/rejected material

Accessible when useful, but not allowed to dominate normal implementation context.

This structure should reduce context waste without hiding authoritative decisions.

---

## Implementation-Harness Setup Gate

The research phase produces enough information to configure an implementation harness, but **the implementation environment is finalized in a separate setup run**.

Sequence:

`Research complete → curated handoff prepared → Implementation Harness Setup → handoff enriched with final environment/run instructions → implementation begins`

Do not force the research run to finalize host-specific tooling that belongs to the setup run.

Conversely, the setup run must not redesign the cognitive platform merely because it prefers a different implementation tool.

---

## Setup Output Required Before Implementation

Before the main implementation run starts, the implementation-harness setup phase should produce or finalize:

- selected harness and version(s);
- target model/main-agent configuration;
- subagent roles/configurations if justified;
- context-management strategy;
- approval/security behavior;
- required local software;
- selected plugins/skills/MCPs/tools;
- repo/bootstrap instructions;
- issue/work tracking strategy where useful;
- test/evaluation-provider setup boundaries;
- reproducible environment configuration;
- smoke/doctor checks;
- final implementation start prompt/instructions;
- final enriched handoff pointers.

These are setup outputs, not universal research requirements.

---

## Implementation Evidence Can Challenge Research

The handoff is authoritative but not infallible.

Implementation may uncover:

- invalid assumptions;
- unexpected performance characteristics;
- missing contracts;
- impractical interfaces;
- dependency cycles;
- better implementation evidence.

The implementation agent must not silently diverge from architecture.

Material contradictions should become explicit ADR/spec-change questions and may trigger a milestone architecture review.

---

## Deferred Work

Research may intentionally defer work that requires unavailable or unjustifiably expensive resources, including heavy accelerator-dependent evaluation.

Deferred items should include, where useful:

- why they were deferred;
- what they would validate;
- required environment/compute;
- prepared configs/data/harness if available;
- success criteria;
- architecture decisions currently depending on the result;
- revisit trigger.

A deferred experiment must not masquerade as completed evidence.

If physical hardware is unavailable but suitable simulation/emulation exists, the relevant test should ordinarily be prepared or executed through that simulation rather than simply marked "hardware unavailable" and skipped. Remaining physical-only validation must be explicit.

---

## System Naming Handoff

The research-program/repository name is not the system name.

If research selects a canonical system name, the handoff should contain:

- selected name;
- rationale;
- intended scope (runtime/platform/framework/etc.);
- obvious collision checks;
- whether the name is already an external compatibility surface.

If naming remains deferred, implementation should continue using neutral terminology until a deliberate decision is made.

---

## Success Standard

The result should not merely be another agent framework.

The intended outcome is a reusable, evidence-driven cognitive systems platform where:

- intelligence can be decomposed;
- components can specialize;
- different model/algorithm families can cooperate;
- hardware can be exploited intelligently;
- deployments can scale in both directions;
- realtime and slow cognition can coexist;
- modules can be reused across materially different applications;
- architectural decisions remain understandable;
- knowledge survives individual AI sessions;
- implementation can evolve without collapsing under its own complexity.

The research process itself should leave reusable knowledge and tooling even when individual architectural candidates are rejected.

---

## Final Handoff Quality Gate

A handoff is not complete if the implementation agent must:

- infer major missing requirements from chat history;
- guess which conflicting document is authoritative;
- load the entire Vault to understand ordinary tasks;
- reverse-engineer module/contract semantics;
- assume unresolved provider/resource constraints;
- invent versioning/security policies that research was supposed to define.

A good handoff should enable implementation to start quickly while preserving an explicit path back to deeper evidence when questions arise.
