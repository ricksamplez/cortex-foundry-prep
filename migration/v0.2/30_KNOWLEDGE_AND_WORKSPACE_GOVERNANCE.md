# Research Workspace & Knowledge Governance

**Status:** modular v0.2 preparation draft  
**Purpose:** define how research knowledge is structured, validated, persisted, and reused.

---

## Research Workspace

The research repository should function as persistent external working memory for the research program and later implementation systems.

An Obsidian-compatible Markdown Vault is encouraged.

However:

**Git and portable files are the knowledge format. Obsidian is a view and editing interface.**

Critical semantics must not depend exclusively on proprietary or fragile Obsidian plugins.

The research run is authorized to design and evolve the final Vault structure when doing so improves clarity, retrieval, validation, or maintainability.

---

## Repository Authority

The research repository is the canonical source for:

- requirements;
- evidence;
- hypotheses;
- assumptions;
- experiments;
- ontology;
- architecture;
- specifications;
- decisions/ADRs;
- module knowledge;
- model/provider suitability knowledge;
- reference-workload analysis;
- implementation handoff;
- open questions;
- important project state/checkpoints.

Chat transcripts are not authoritative project state.

Project Docs may provide stable bootstrap context, but canonical evolving knowledge belongs in the repository.

---

## Canonical State and Checkpoints

Long-running work should leave durable checkpoints throughout a turn.

Checkpointing should capture meaningful completed work rather than dump every conversational step.

Prefer:

- current-state files updated in place;
- atomic commits/checkpoints;
- ADRs for meaningful decisions;
- experiments for empirical work;
- explicit unresolved-question artifacts;
- bounded logs/ledgers when chronological append-only data is genuinely useful.

A restart or context loss should require rehydrating repository state, not reconstructing the project from chat memory.

---

## Bounded File Growth

The repository must not evolve into giant mutable files that append every research round forever.

Current-state knowledge should be updated in place or decomposed by semantic boundary.

Historical information should be preserved using appropriate mechanisms such as:

- Git history;
- ADRs;
- experiments;
- changelogs;
- archives;
- sharded logs;
- rotated ledgers.

Append-only artifacts must use deterministic rotation/sharding.

The research program must establish an explicit measurable file-size/complexity policy early enough to prevent pathological growth.

The exact thresholds are intentionally not predetermined.

The policy should optimize for:

- efficient AI retrieval;
- human readability;
- clean diffs;
- fast indexing;
- independent modification;
- limited context loading.

Large generated artifacts may use different handling when justified, but the exception must not become an excuse for unbounded mutable knowledge files.

---

## Canonical Extensible Ontology

The project requires an extensible ontology covering relevant concepts, capabilities, module relationships, events, actions, providers, profiles, and other entities.

The ontology must avoid uncontrolled duplicate concepts.

Before a new canonical term/identifier is accepted, perform canonicalization and semantic collision/equivalence checks against existing entries.

The ontology should be able to represent relationships comparable to:

- alias;
- equivalent;
- broader;
- narrower;
- related;
- supersedes;
- deprecated by.

Different entity classes must not be conflated.

For example, the following may be related without being identical:

- conceptual idea;
- capability;
- capability provider;
- module;
- extension point;
- event;
- executable action;
- profile/reference system.

Canonical identifiers should be stable and machine-readable.

Aliases must not become accidental duplicate canonical concepts.

The ontology must be extensible without requiring destructive renaming of unrelated concepts.

---

## Research Artifacts vs Implementation

Research findings and implementations must remain distinguishable.

A promising concept must not disappear because it was not selected for the first implementation.

Preserve, where useful:

- researched concepts;
- candidate modules;
- implemented modules;
- rejected approaches;
- experiments;
- unresolved questions;
- revisit conditions.

"Rejected" does not mean "delete".

A rejected approach should record enough context to avoid repeating known mistakes and to recognize when changed conditions justify revisiting it.

---

## Documentation as a Product Requirement

Important architecture, modules, experiments, interfaces, deployment behavior, failures, and decisions must be documented.

Documentation should support both:

- humans;
- capable AI coding/research agents.

Prefer progressive disclosure over giant documents.

Canonical facts should have one authoritative location where practical.

Other documents should link/reference canonical information instead of copying it unless duplication is intentionally generated and mechanically synchronized.

---

## Module Documentation Standard

Every implemented reusable module must have both:

1. a structured machine-readable **Module Card**;
2. a human- and agent-readable `README.md`.

Documentation is part of module completeness.

### Module Card

The exact schema is a research decision, but it should ultimately make it possible to discover/evaluate properties such as:

- canonical identity;
- purpose;
- provided capabilities;
- required capabilities;
- extension points/contributions;
- inputs;
- outputs;
- state requirements;
- supported execution modes;
- hardware/resource requirements;
- latency class;
- concurrency;
- idempotency;
- dependencies;
- privileges;
- security properties;
- known failure modes;
- observability;
- supported platforms;
- routing/workflow behavior where relevant;
- evaluation;
- compatibility;
- lifecycle state;
- version;
- provenance;
- license;
- relevant evidence.

### README

The README should explain:

- what the module does;
- why it exists;
- when to use it;
- when not to use it;
- how to integrate it;
- important trade-offs;
- known limitations;
- failure modes;
- relevant alternatives;
- evaluation methodology;
- important architecture decisions;
- links to relevant research/evidence.

Module documentation should remain understandable without requiring the reader to reverse-engineer code or chat history.

---

## Model Suitability Knowledge Base

Preserve reusable guidance about which models/model classes/families are appropriate for specific capabilities, modules, and optional module features.

The knowledge base should not reduce suitability to one simplistic `minimum_model_size` field.

When evidence supports it, capture:

- adequate model size/class range;
- when a larger class becomes necessary;
- known strong model families;
- known weak/unsuitable families;
- exceptions by model family;
- quantization sensitivity;
- reasoning requirements;
- latency implications;
- effective-cost implications;
- reliability/failure patterns;
- confidence;
- evidence;
- revisit conditions.

### Functional capability requirements

Suitability must also account for required model functionality, including where relevant:

- tool use/function calling;
- structured output / schema adherence;
- vision;
- image/video input;
- audio/speech input;
- speech/audio output;
- native multimodality;
- streaming;
- long context;
- embeddings;
- reranking;
- statefulness;
- realtime suitability;
- action/control output;
- provider/runtime-specific constraints.

### Per-feature requirements

Requirements may differ between a module's base function and optional/advanced features.

For example:

- base capability may work with a good small text model;
- optional visual feature may require vision;
- advanced tool workflow may require reliable tool calling/structured output;
- speech feature may require audio input/output;
- high-complexity mode may require a larger reasoning class.

The knowledge representation must support feature-level requirements and conditional recommendations rather than one global model label per module.

### Negative knowledge

Document known unsuitable/unsafe choices when evidence is strong enough.

A statement such as "family Z is not recommended for this structured streaming tool workflow under these conditions" can be as valuable as a positive recommendation.

---

## Provider Capacity Snapshots

Provider limits change over time and should not be hardcoded into permanent architecture documents.

Maintain time-stamped provider-capacity snapshots when provider availability/capacity materially affects evaluation or implementation planning.

Capture relevant **guaranteed or normal plan/account limits** such as:

- requests per minute;
- tokens per minute;
- daily quotas;
- concurrency;
- rolling-window limits;
- multi-hour windows such as 5-hour usage;
- weekly limits;
- monthly limits where applicable;
- model-specific restrictions;
- reasoning-specific restrictions;
- free-credit/quota state;
- reset semantics;
- context/input/output limits where relevant;
- source;
- checked-at timestamp.

### Guaranteed-capacity rule

Do **not** count saved/banked resets, opportunistic bonus resets, temporary promotional capacity, or similar non-guaranteed mechanisms as dependable provider capacity.

Plan capacity is plan capacity.

Bonus capacity may be observed elsewhere if operationally useful, but it must not inflate the resource assumptions used by architecture/planning.

---

## Open-Question Persistence

Important non-blocking uncertainty must be persisted.

The exact schema may evolve, but the workspace should be able to represent information comparable to:

- stable question ID;
- question;
- discovery time;
- status;
- blocking/non-blocking;
- priority/impact;
- current best answer;
- confidence;
- needed evidence;
- related requirements/ADRs/modules;
- revisit trigger.

Do not force all open questions into one permanently growing monster file.

Use indexes plus semantic sharding or another bounded structure when scale requires it.

---

## Evidence and Source Ledgers

Where append-only evidence/source tracking is useful, it must remain bounded and deterministic.

Possible approaches include time-based or size-based shards plus generated indexes.

The exact representation should support:

- source identity;
- retrieval/access date;
- provenance;
- evidence class/quality where useful;
- affected claims/decisions;
- de-duplication;
- archival/retrieval.

Do not duplicate large source content merely to create provenance records.

---

## Generated Indexes and Knowledge Views

The workspace may create generated indexes, graphs, maps-of-content, search indexes, or other views to improve navigation.

Generated views must not become competing authorities for canonical facts unless their generation process explicitly defines them as such.

Where possible, generated artifacts should be reproducible from canonical source files.

---

## Validation and Consistency

The research program may implement validators/helpers for:

- ontology collisions;
- broken links;
- schema compliance;
- missing Module Cards/READMEs;
- invalid canonical identifiers;
- inconsistent version metadata;
- duplicate sources;
- unresolved references;
- file-growth policy;
- migration/coverage checks;
- stale generated indexes.

The exact tooling is intentionally not prescribed.

Validation should reduce silent drift without making ordinary editing unnecessarily brittle.

---

## Portability

The knowledge base should remain usable without one proprietary desktop application, database, or model vendor.

Obsidian-specific conveniences are allowed when they are optional views over portable canonical files.

The repository should remain inspectable through ordinary Git/filesystem tooling and understandable by future human or AI maintainers.
