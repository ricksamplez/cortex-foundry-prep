# Preparation Baseline

## Source charter

The current frozen source document supplied by the owner is:

`Cortex Foundry — Requirements Charter & Research Program Definition v0.1.md`

Observed local source properties at preparation time:

- SHA-256: `8b2731602fd968c046045c49b1fd194c432f594dc171cb1482137b987c7335c4`
- size: `44,635` bytes
- line count reported by `wc -l`: `1,683`

The source charter remains the **loss-prevention baseline** while preparing its modular successor.

## No-loss migration invariant

No existing requirement, constraint, permission, research question, completion criterion, or meaningful nuance from v0.1 may silently disappear during restructuring.

For every source section/content unit, the modular successor must either:

1. retain it in an appropriate canonical document;
2. replace it with an explicitly stronger or more precise requirement; or
3. mark a deliberate semantic change with rationale.

Create a section/content migration map before declaring the modular successor complete.

## Planned split

The original all-in-one charter should be decomposed so each later run receives only relevant material.

Expected logical families:

- core requirements / architecture invariants;
- research program and autonomy contract;
- reference workloads;
- research workspace/governance;
- research completion and implementation handoff requirements;
- separate Implementation Harness Setup runbook;
- separate Architecture Review runbook.

The exact file layout remains a bootstrap-design decision, but run-specific material must not be needlessly injected into unrelated contexts.

## Model-name hygiene

Research and architecture-review instructions should address the model directly (`you`) or by role/function, not tell it that it is a specific elite model. The goal is to avoid status/identity priming and keep conclusions grounded in evidence and requirements.

The implementation-target model may be explicitly named where technically relevant. GPT-6 Astra is the current primary target for the implementation harness.
