# Milestone Architecture Review Runbook

**Status:** modular v0.2 preparation draft  
**Scope:** separate review chats/runs used only at meaningful implementation milestones.

---

## Review Role and Scope

Act as an independent architecture/code reviewer.

Primary questions:

- Is the implementation still solving the intended problem?
- Does it satisfy authoritative requirements?
- Has implementation silently diverged from architecture/contracts?
- Has implementation evidence invalidated a research assumption?
- Are important edge cases, failure modes, integrations, security boundaries, or evaluation gaps missing?
- Has implementation introduced unnecessary coupling or broken modularity?
- Are performance/latency/resource assumptions still plausible?
- Are documentation/module/compatibility obligations being met?

The specification is authoritative but not infallible.

Implementation evidence may reveal that the specification itself is wrong.

Do not force implementation back into an invalid design merely because an earlier architecture document said so.

---

## Review Model-Name Hygiene

Address the reviewer directly by role/function.

Do not prime the reviewer with statements that it is a specific elite model/version or imply that status makes its conclusions superior.

The target implementation model/harness may be named when relevant to understanding the implementation.

---

## Review Trigger and Checkpoint

Architecture review should occur only at **architecturally meaningful milestones**, not after every small change.

Potential trigger classes include:

- stabilization of core contracts;
- first end-to-end vertical slice;
- completion/integration of major module/runtime systems;
- routing/resource/execution subsystem integration;
- state/context/memory subsystem integration;
- first serious reference-workload slice;
- major architecture migration;
- pre-release or major implementation handoff.

The exact milestone schedule should follow the actual architecture/implementation plan.

### Stable checkpoint requirement

Review a stable commit/checkpoint.

The live implementation agent must be paused while the review runs so architecture/spec/issues do not change underneath the review.

Inputs should include as relevant:

- reviewed commit SHA;
- authoritative requirements;
- relevant architecture/spec;
- ADRs;
- implementation summary;
- tests/eval results;
- open issues/questions;
- known deviations;
- previous review findings still relevant.

---

## Comprehensive Review per Campaign

A review campaign should attempt to cover the meaningful milestone scope in one expensive review turn/run.

Do **not** stop after finding the first valid issue.

Continue reviewing independent areas while useful work remains and tool/context limits allow.

One review campaign may correctly produce:

- zero issues;
- one issue;
- many issues.

There is no one-message/one-issue constraint.

---

## Finding Validation

Before creating an engineering issue:

1. identify the suspected defect/gap/conflict;
2. inspect relevant code/spec/evidence;
3. determine materiality;
4. reproduce or establish evidential support where appropriate;
5. check whether an existing issue already covers it;
6. decide whether it belongs with related findings or deserves an independent unit of work.

Avoid issue spam for:

- purely stylistic preferences;
- speculative concerns with no meaningful evidence;
- duplicate findings;
- trivial changes that can be fixed immediately without cross-run value.

---

## Finding Classes

The exact taxonomy may evolve, but review should distinguish concepts such as:

- architecture defect;
- requirement violation;
- contract/schema violation;
- spec conflict;
- integration gap;
- security/trust issue;
- performance/latency/resource issue;
- reliability/failure-mode gap;
- evaluation gap;
- documentation/compatibility gap;
- technical debt with material architectural consequence;
- research/open question.

Severity/blocking semantics should be explicit enough for the implementation run to prioritize correctly.

---

## Issue Workflow

When GitHub write access is available, create zero-to-many issues directly from validated review findings.

An issue should normally be:

- actionable;
- reproducible or evidentially supported;
- materially relevant;
- sufficiently scoped.

Include where applicable:

- concise title;
- finding class;
- severity;
- blocking/non-blocking status;
- affected requirement;
- affected ADR/contract/module;
- evidence;
- reviewed commit/reference;
- reproduction steps;
- expected behavior;
- observed behavior;
- architecture/spec implications;
- acceptance criteria;
- validation/retest expectations;
- relevant links.

Similar findings should be deduplicated.

Related findings should be grouped when one fix/verification unit is appropriate.

Independent fixes should remain independent issues when grouping would obscure ownership/acceptance.

Issues are an engineering queue/control surface, not a transcript dump.

---

## Spec-Conflict Path

When implementation evidence suggests the **specification or architecture is wrong**, do not write an issue that blindly demands code conform to the bad spec.

Instead:

- identify the conflicting evidence;
- state which requirement/ADR/spec is affected;
- determine whether the conflict is local or architectural;
- create an explicit spec/architecture question or change request;
- preserve current implementation state;
- require deliberate resolution before broad follow-on work if the conflict is blocking.

The review system must be willing to revise its own previous assumptions.

---

## Review of Tests/Evals

Review should inspect whether tests/evaluations actually prove the claimed behavior.

Look for:

- missing failure/degraded cases;
- unrealistic fixtures;
- absent concurrency/race tests where relevant;
- incomplete contract/version tests;
- provider/model assumptions hidden in mocks;
- missing latency/resource measurements;
- false confidence from one happy-path vertical slice;
- missing replay/idempotency/cancellation tests;
- insufficient security/permission coverage;
- gaps in reference-workload acceptance criteria.

Do not demand exhaustive testing unrelated to milestone risk.

---

## Review of Documentation/Governance

Where relevant verify:

- Module Cards exist and match implementation;
- module `README.md` files are complete enough;
- ontology/canonical IDs remain consistent;
- extension/contribution points are documented;
- versioning/migration implications are handled;
- new provider/model suitability evidence is persisted;
- important implementation decisions have ADR/spec updates;
- no giant append-only knowledge artifacts are accumulating.

---

## Review Completion

A milestone review is complete when:

- the intended milestone scope has been inspected sufficiently;
- validated findings are persisted;
- duplicates have been removed/grouped;
- blocking spec conflicts are explicit;
- zero-to-many issues/change requests have been created as appropriate;
- a concise review summary/checkpoint exists;
- the implementation run has a clear resumption state.

Then the implementation run may resume.

Do not keep implementation paused for unrelated research once the milestone review is complete.
