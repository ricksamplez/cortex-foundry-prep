# Research Pre-Launch Audit

**Status:** preparation checklist before initializing/populating the real research repository and starting the first Research run.

## A. Migration integrity

- [x] Frozen v0.1 source fingerprint verified.
- [x] All 62 v0.1 numbered sections mapped.
- [x] Zero v0.1 sections marked dropped.
- [x] All migration destination file/anchor references resolve.
- [x] 30 persisted post-v0.1 decisions mapped.
- [x] Zero mapped post-v0.1 decisions remain pending.
- [x] Non-trivial semantic changes documented.
- [x] Research-program/repository naming boundary preserved.

Detailed proof: `migration/v0.2/MIGRATION_AUDIT.md`.

## B. Run isolation

- [x] Research Program Contract excludes implementation-host setup details.
- [x] Implementation Harness Setup is a separate runbook.
- [x] Architecture Review is a separate milestone runbook.
- [x] Research/Review docs do not tell the model that it is GPT-6 Pro.
- [x] GPT-6 Astra may be named where it is technically the implementation target.
- [x] No preparation-workspace name/URL appears in future-facing modular draft docs.

## C. Project Docs

- [x] Compact Project Context drafted.
- [x] Project Docs manifest drafted.
- [x] Core Requirements draft exists.
- [x] Research Program Contract draft exists.
- [x] Reference Workloads draft exists.
- [x] Knowledge/Workspace Governance draft exists.
- [x] Research Completion/Handoff draft exists.
- [x] Setup/Review runbooks excluded from initial Research Project Docs.

## D. Project Custom Instructions

- [x] Concise behavior-level instructions drafted.
- [x] No architecture duplication.
- [x] Maximum useful work/turn behavior included.
- [x] Assumption/non-blocking-question behavior included.
- [x] Repository authority/checkpointing included.
- [x] Container-first / Actions-fallback rule included.
- [x] `Please continue.` protocol included.
- [x] First run instructed to perform substantive work, not only planning.

## E. Real-repo bootstrap design

- [x] Minimal seed layout designed.
- [x] Future-facing root README drafted.
- [x] Future-facing Project Context drafted.
- [x] Current State seed drafted.
- [x] Next Work seed drafted.
- [x] Open Questions seed drafted.
- [x] Deeper Vault taxonomy intentionally left for the Research run to design.
- [x] Setup/Review runbooks intentionally excluded from initial Research seed.

## F. Research Start Contract

- [x] Canonical repo identified.
- [x] Project Docs inspection required.
- [x] Minimal Vault bootstrap required.
- [x] Dependency-aware research map required.
- [x] Real research must begin in the first turn.
- [x] External repositories/public skill registries allowed as evidence.
- [x] Research helpers allowed.
- [x] Frequent persistence/checkpoints required.
- [x] Heavy accelerator work deferred.
- [x] Full implementation explicitly gated.
- [x] Maximum useful work per expensive message required.
- [x] Continuation protocol included.

## G. Still required before launch

- [x] Perform final assistant editorial pass over the five modular docs.
- [ ] Decide whether any wording should change before calling them v0.2 rather than preparation drafts.
- [x] Copy modular v0.2 candidate docs into the real-repo seed tree.
- [ ] Create the coherent initial bootstrap commit in `ricksamplez/cortex-foundry`.
- [ ] Add/upload the selected Project Docs to the dedicated project-only-memory ChatGPT Project.
- [ ] Set the prepared Project Custom Instructions.
- [ ] Verify GitHub write access from the actual Research chat.
- [x] Run one final leak scan on the exact files/prompts being handed to the Research run.
- [ ] Send the Research Start Contract as the first user message.

## Launch rule

Do not launch the expensive Research run while any material item in section G is unresolved.

Preparation-only history must not be copied into the real repository.

The real repository should start from the coherent approved bootstrap state.
