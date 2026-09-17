# Cortex Foundry — Preparation Workspace

Private-to-the-planning-process workspace for preparing the Cortex Foundry research program, project bootstrap, run contracts, and handoff material.

## Hard boundary

This repository is **preparation-only**.

- It must never be exposed to, referenced by, linked from, or mentioned to any later research, implementation-harness-setup, implementation, or architecture-review run.
- Its repository name/URL and its existence must not leak into generated Project Docs, runbooks, prompts, handoffs, source ledgers, or the eventual `ricksamplez/cortex-foundry` repository.
- Later runs receive only explicitly curated artifacts copied/reworked from here.
- Before any handoff, perform a leak check for this repository name, URL, and preparation-only terminology.

## Purpose

Persist the evolving plan so that decisions do not remain trapped in chat history while the final Project/Repo bootstrap is still being designed.

This workspace may contain:

- frozen source/baseline notes;
- requirement deltas and migration maps;
- run-boundary decisions;
- implementation-host/provider policy notes;
- reference-workload design notes;
- bootstrap planning;
- preparation-only assumptions and TODOs.

It is **not** the canonical Cortex Foundry research Vault and must never be treated as such by later runs.

## Current next step

Use the persisted preparation state to produce a lossless modular successor to the original Requirements Charter, then design the Project-/Repo-Bootstrap and Research Start Contract for the first WebUI research run.
