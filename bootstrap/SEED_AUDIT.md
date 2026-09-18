# Seed / Cutover Audit

**Status:** passed for the prepared real-repo seed and first-run handoff files.

## Real target repository

Target: `ricksamplez/cortex-foundry`

Observed before cutover:

- private;
- default branch: `main`;
- repository size reported as `0`;
- no existing bootstrap content was found.

The target repository remains untouched by this preparation audit.

## Prepared seed

Prepared future-facing seed files: **10**

- `README.md`
- `PROJECT_CONTEXT.md`
- `state/CURRENT_STATE.md`
- `state/NEXT_WORK.md`
- `state/OPEN_QUESTIONS.md`
- `docs/00_CORE_REQUIREMENTS_CHARTER.md`
- `docs/10_RESEARCH_PROGRAM_CONTRACT.md`
- `docs/20_REFERENCE_WORKLOADS.md`
- `docs/30_KNOWLEDGE_AND_WORKSPACE_GOVERNANCE.md`
- `docs/40_RESEARCH_COMPLETION_AND_HANDOFF.md`

## Seed scope checks

- preparation-workspace name/URL leaks: **0**
- explicit `GPT-6 Pro` identity mentions: **0**
- Implementation Harness Setup runbook files included: **0**
- Architecture Review runbook files included: **0**
- Project Context drift between Project and repo copies: **0**

## First-run handoff checks

The actual files intended for direct use by the first Research run are clean:

- `bootstrap/run/RESEARCH_START_CONTRACT.md`
- `bootstrap/project/CUSTOM_INSTRUCTIONS.md`
- `bootstrap/project/PROJECT_CONTEXT.md`

Checks:

- preparation-workspace name/URL leaks: **0**
- explicit `GPT-6 Pro` identity mentions: **0**
- setup/review runbook content injected into the first-run prompt: **0**
- full implementation start requested prematurely: **no**
- first run required to begin substantive research after bootstrap: **yes**

`PROJECT_DOCS_MANIFEST.md` intentionally names the setup/review runbooks only to state that they are **excluded**; it is a preparation/design artifact and is not itself handed to the Research run.

## File-size sanity

Largest prepared seed document is the Core Requirements Charter at roughly 21.6k characters.

No seed state/log file is large.

The future Research run remains responsible for creating an explicit measurable file-size/complexity policy.

## Cutover readiness

The prepared seed is technically ready to populate the real research repository after final approval of the modular v0.2 candidate wording.

Recommended history objective:

- create the real repository bootstrap as coherently as the available GitHub write interface permits;
- avoid copying preparation history;
- do not copy migration maps/audits/runbooks into the initial Research workspace;
- introduce setup/review runbooks only when those phases begin.

## Remaining external/manual setup

Before launching the first Research run:

- populate the real repository with the approved seed;
- create/configure the dedicated project-only-memory ChatGPT Project;
- add the approved Project Docs;
- set the prepared Custom Instructions;
- verify GitHub write access from the actual Research chat;
- send the Research Start Contract as the first message.
