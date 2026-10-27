# AI VTuber v1 — Technical Blueprint Spec

**Projektkontext:** Ein einzelner AI-VTuber-/AI-Performer-Charakter mit 3D-Avatar, Voice, Twitch/Matrix, FL-Studio-/Music-Production-Begleitung, Memory, Filter, Tooling, Mission Control und späterer Erweiterbarkeit auf weitere Modi/Charaktere.

**Status:** Konsolidierte Markdown-Fassung nach Canvas-Limit.  
**Leitidee:** Kein Monster-Prompt, kein Monolith, sondern eine modulare Live-Character-Production-Platform.

---

## 0. Executive Summary

v1 ist ein **reales, streambares Live-System** für einen AI-Charakter, nicht die finale Neuro/Evil-Klasse.

Die Architektur trennt strikt:

- **NATS/JetStream** = internes Nervensystem / Event-Bus
- **Temporal** = langlebige, crash-feste Workflows
- **PostgreSQL** = operativer Datenkern
- **pgvector + pgvectorscale** = semantische Memory-Suche
- **pgrouting** = Graph-Memory-Beziehungen, falls nützlich
- **Rolling-Context-DAG** = historische Karte, nicht Hauptmemory
- **Typed Memory** = eigentliches Arbeits-/Langzeitmemory
- **Mission Control** = ein einziges Operator-Frontend
- **Grafana lokal/Docker** = eingebettete oder separate Debug-/Audit-/Observability-Panels, nicht Control Plane
- **Avatar-Control Contract** = austauschbare Driver für Warudo und Unity
- **FL Studio Bridge** = DAW als virtuelle AI-Control-Surface
- **Mode Manager** = nahtlose Stream-/Arbeitsmodi inklusive Twitch-Kategorie-Handling
- **Output Filter** = externes zweistufiges Filter-/Cut-System
- **Fine-Tune Capture** = automatische Rohdaten-/Request-Response-Erfassung, manuelle Kuration

---

## 1. Purpose

Dieses Dokument definiert den technischen v1-Blueprint für ein single-character AI-VTuber-/AI-Performer-System mit:

- 3D-Avatar-Ausgabe über Warudo als Interim-Option und später Unity
- deutscher Hauptsprache, englischer Zweitsprache
- lokaler ASR/STT-Route
- lokaler TTS-Route
- Cloud-Main-LLM mit Open-Weights-Langfristpfad
- Twitch + Matrix zuerst
- FL-Studio-/Music-Production-Begleitung
- event-driven async Backend in Python
- Mission Control / Director Mode
- mehrschichtigem, editierbarem Memory
- Rolling-Context-DAG für historische Rückverfolgung
- automatischer Fine-Tune-Datenerfassung
- Filter, Subtitles, Watchdog, Supervisor und Degraded Modes

---

## 2. Goals

### 2.1 Primary Goals

1. Einen glaubwürdigen einzelnen AI-Performer in Live-Situationen erzeugen.
2. Live Voice, Stream-Chat, Plattform-Events, DAW-State und Avatar-State zusammenführen.
3. Latenz niedrig genug für Dev-Streams und frühe öffentliche Streams halten.
4. Hot Paths stabil, cancellable und observierbar bauen.
5. Charakterkontinuität über Sessions hinweg erhalten.
6. Memory vollständig operator-editierbar machen.
7. Fine-Tune-Kandidaten automatisch erfassen, aber manuell kuratieren.
8. Moduswechsel nahtlos machen.
9. Music-Production-Streams ohne schweres Realtime-Music-Understanding ermöglichen.
10. Für späteren zweiten Charakter und weitere Modi vorbereiten.

### 2.2 Non-Goals für v1

1. Arbiträre Game-Autonomie auf Neuro-Endgame-Niveau.
2. Singing als Teil des normalen TTS-Pfades.
3. Learned Full-Body Motion Generation.
4. Discord-Voice-Parität.
5. Vollständig lokaler Main-LLM-Betrieb.
6. Vollautomatische, nicht-reviewte Dreaming-/Canon-Promotion.
7. Komplexe Multi-Agent-Simulation.
8. Realtime-Audio-Music-Understanding als Pflichtfeature.

---

## 3. Design Principles

1. **Event-driven over request-chained monoliths**
2. **Async orchestration over sync pipelines**
3. **Small specialized subsystems over one magic model**
4. **Deterministic rules on hot paths, LLM judgment on richer paths**
5. **Editable memory over opaque auto-canonization**
6. **Engine telemetry over vision when internal world state already exists**
7. **Graceful degradation over hard failure**
8. **One-character v1, two-character-ready scheduler**
9. **Operator control over hidden autonomy**
10. **Replayability over “works on my machine” confidence**
11. **Typed contracts over ad-hoc payload sprawl**
12. **Feature-flagged rollout over big-bang behavior changes**
13. **Character agency over obedience**
14. **Typed memory over prompt soup**
15. **Raw event store as truth, summaries as maps**

---

## 4. High-Level Architecture

### 4.1 Runtime Model

Das System läuft verteilt über mehrere Rechner:

#### Machine A — Main Compute Host

- Python-Orchestration
- NATS/JetStream Clients
- Main LLM Gateway
- ASR/STT Worker
- TTS Worker
- Output Filter
- Memory Services
- Tool/Search Services
- Prompt Compiler
- Temporal Workers
- Mission Control Backend
- Supervisor

#### Machine B — Avatar / OBS Host

- Warudo interim oder später Unity Runtime
- Avatar Rendering
- OBS
- Avatar Driver
- VMC/OSC falls nötig
- Game Source / Capture Source

#### Machine C — optional Game/Worker Host

- isolierte Game-Instanzen
- Game Capture / Telemetry
- extra Worker

#### Optional VPS

- leichte Services
- externe Erreichbarkeit
- Bridge-/Webhook-Komponenten
- kein zwingender Hot-Path-Knoten

---

## 5. Dev Baseline / Local Bootstrap

Before feature work starts, the project needs a boring but reliable local baseline.

Minimum baseline:

- Docker Compose stack for local development
- `.env.example` and typed settings
- clear local secrets handling
- database migrations
- shared contracts/schemas package
- structured logging from the beginning
- local start/stop scripts
- basic test runner
- local health checks
- minimal seed data where useful

Recommended config direction:

- Pydantic Settings or equivalent typed config
- environment-specific config files only where needed
- no secrets in repo
- one clear place for service URLs, ports, feature flags, model routes, and local paths

Reason:

The architecture has many moving parts. A stable dev baseline prevents the project from turning into “which terminal did I start this in again?” chaos.

---


## 6. Backup / Restore / Disaster Recovery

### 6.1 Purpose

The system accumulates long-term value in memory, behavior assets, fine-tune captures, stream history, prompt traces, project memory, and operator interventions. Backups are therefore part of v1, not a luxury add-on.

### 6.2 Data classes to back up

Must be covered:

- PostgreSQL operational database
- behavior asset versions
- typed memory and graph-memory tables
- Rolling Context DAG metadata
- prompt traces and prompt package versions
- approval/action journals
- Temporal workflow state and visibility data according to deployment strategy
- JetStream retained stream configuration and important retained event streams
- fine-tune capture folders
- media artifacts referenced by manifests
- Mission Control configuration and feature-flag snapshots

### 6.3 Backup policy

Baseline policy:

- daily PostgreSQL logical or physical backup
- regular backup of media/fine-tune capture folders
- behavior asset versions backed up on every activation/change
- backup manifests should include schema/app version, timestamp, host, and checksum metadata
- backups should be stored outside the primary runtime directory
- no backup is trusted until restore has been tested

### 6.4 Restore policy

Define a minimal recoverable system:

1. PostgreSQL schema and data restored
2. behavior assets restored
3. Mission Control can start
4. NATS/JetStream can start or be rehydrated to a safe empty/degraded state
5. Temporal can resume or workflows can be safely marked failed/restarted
6. memory and prompt traces remain inspectable
7. fine-tune capture manifests still resolve to files

### 6.5 Disaster recovery tests

At minimum:

- periodic restore into a separate local test namespace
- verify DB migrations after restore
- verify Mission Control can read memory/version/asset data
- verify at least one fine-tune capture bundle resolves
- verify a replay bundle can be loaded
- verify broken/missing artifacts are reported clearly instead of failing silently

## 7. Core Logical Layers

1. Input Adapters
2. Perception Layer
3. Attention / Turn / Floor Layer
4. Cognition Layer
5. Tool / Search / Action Layer
6. Safety / Filter Layer
7. Render / Output Layer
8. Avatar Control Layer
9. Memory Layer
10. Rolling-Context-DAG Layer
11. Fine-Tune Capture Layer
12. Supervisor / Observability Layer
13. Mission Control Layer

---

## 8. Event Bus and Transport

### 8.1 Primary Bus

**NATS Core + JetStream**

#### NATS Core für:

- Realtime Events
- Hot-path Broadcasts
- Presence
- Avatar State
- VAD / speech events
- short-lived signals

#### JetStream für:

- replayable streams
- important state transitions
- tool calls/results
- filter events
- memory candidates
- supervisor incidents
- stream events
- durable event logs

### 8.2 Event Classes

#### Ephemeral Subjects

- VAD activity
- speaking state
- avatar state ticks
- live emotion state
- OBS scene state
- presence heartbeats
- subtitle fragments

#### Durable Streams

- raw utterance events
- finalized ASR segments
- committed assistant outputs
- filter actions
- tool calls/results
- memory candidate events
- platform events
- FL Studio state/action events
- operator interventions

### 8.3 Delivery Rules

- Hot-path signals prefer low overhead.
- Important state transitions are persisted.
- Every assistant output chunk has `track_id`.
- Every tool/action call has `action_id`.
- Durable events include timestamps, source tags, trace IDs.
- Long-lived workflows are escalated to Temporal.

---

## 9. Interface Strategy

Nicht alles wird auf WebSockets gezwungen.

### 9.1 Rules

- **Mission Control Frontend ↔ Backend:** realtime connection / WebSocket-style updates.
- **Mission Control Backend ↔ internal services:** NATS/JetStream and service-native calls.
- **Temporal:** Temporal SDK / client model.
- **OBS:** OBS WebSocket.
- **FL Bridge:** WebSocket, UDP/OSC, MIDI/Sysex oder stabilster praktischer Pfad.
- **Downloads/Exports/Health/CRUD:** HTTP/REST-style endpoints sind erlaubt.
- **Grafana:** Observability-only, lokal, eingebettet wo sinnvoll.

### 9.2 Goal

Weniger Protokoll-Sprawl, aber kein WebSocket-Kult.

WebSockets sind gut für:

- UI live state
- bidirektionale Control Sessions
- interaktive Bridges

HTTP bleibt gut für:

- Downloads
- Dataset Exports
- Health Checks
- Webhooks
- CRUD
- statische Assets
- one-shot Admin Actions

---

## 10. Event Contracts

Jedes Event sollte enthalten:

```json
{
  "event_id": "uuidv7",
  "trace_id": "uuidv7",
  "correlation_id": "uuidv7",
  "causation_id": "uuidv7|null",
  "source": "twitch|speech|fl_studio|obs|avatar|tool|operator|...",
  "subject": "string",
  "event_type": "string",
  "priority": "low|normal|high|critical",
  "created_at": "timestamp",
  "monotonic_offset": "optional",
  "schema_version": "int",
  "payload": {}
}
```

### 10.1 Goals

- safe replay
- schema evolution
- debugability
- traceability
- auditability

---

## 11. Mission Control

### 11.1 Grundsatz

Mission Control ist **ein einziges kohärentes Frontend**.

- Primäre v0/v1-Basis: **NiceGUI**
- Grafana läuft lokal in Docker.
- Grafana darf Panels/Graphs liefern, aber keine kritischen Controls.
- Kritische Live-Daten und Controls sind native Mission-Control-Komponenten.
- Audit-/Debug-/Deep Monitoring darf in Grafana bleiben und muss nicht in Mission Control auftauchen.

### 11.2 Local PIN Auth

Mission Control runs only on the local network.

Auth model:

- simple PIN gate
- no visible username required
- local-only by default
- no public exposure without an external reverse-proxy/auth decision
- operator actions still create audit log entries
- failed PIN attempts should be rate-limited enough to avoid accidental spam, not treated like internet-facing auth

Reason:

Mission Control can mute audio, stop TTS, change modes, edit memories, toggle tools, and activate behavior versions. Even on the LAN, it should not be an open red button.

### 11.3 Why NiceGUI

NiceGUI passt für v0/v1, weil:

- Python-first
- schnell baubar
- realtime UI-Updates möglich
- gute Eignung für interne Control Panels
- Backend-Logik nahe am Python-System
- ausreichend für operator-first Tooling

Nicht als öffentliches High-Traffic-Frontend gedacht.

### 11.4 Grafana Role

Grafana:

- lokal/Docker
- Observability
- Dashboards
- Logs/Metrics/Traces
- Panels optional eingebettet
- kein Live-Control-Layer

Grafana-Panels nur einbetten, wenn sie im Stream-/Operator-Kontext wirklich gebraucht werden.

### 11.5 System Dashboard

Zweck: Entwicklung, Debugging, Config, Memory, Workflows, Modellrouten, Health.

Panels:

- Service Health Matrix
- NATS/JetStream Status
- Temporal Workflow Overview
- Model Route Latencies
- Memory Review Queue
- Behavior Asset Versions
- Feature Flags
- Recent Incidents
- Storage/Retention Overview
- Fine-Tune Capture Manifests
- Mode Manager State
- Shared Calendar / Project Timeline Preview

### 11.6 Live Director Dashboard

Zweck: Stream-safe, wenig Clutter, schnelle Eingriffe.

Controls:

- Force Silence
- Stop Current Track
- Flush Queued Tracks
- Disable/Enable Proactivity
- TTS Mute
- STT Mic Mute
- Stream Mic Mute
- Disable Tools/Search/Vision
- Recording Active Indicator
- OBS Scene State
- Current Floor Owner
- Current TTS Track
- Active Degraded Services
- Chat Pressure
- Queued Social Obligations
- One-click Incident Note

Regel:

> Live Director Dashboard priorisiert große Controls, minimale Leselast und schnelle Eingriffe.

### 11.7 Mission Control Feature Areas

#### Live Operations

- mute/unmute TTS
- force silence
- stop track/all tracks
- flush queue
- toggle proactivity
- toggle tools/search/vision/memory promotion
- set degraded mode
- restart safe workers/adapters
- switch modes manually
- apply Twitch metadata manually

#### Runtime Inspection

- current floor owner
- output queue
- active response track
- active model route
- feature flags
- worker health
- service lag/backlog
- active Temporal workflows

#### Memory Control

- inspect provenance
- edit/delete/tombstone memory
- approve/reject promotions
- pin canon
- inspect typed memories
- inspect project memories

#### Version Control

- list behavior asset versions
- show active version
- explicit activation only
- lock old versions
- change notes
- replay/shadow comparison

#### Fine-Tune Capture

- list capture manifests
- browse route/day/stream bundles
- mark bundles for manual review
- export after manual approval

---


## 12. Approval Queue

### 12.1 Purpose

Approval is a first-class subsystem, not scattered ad-hoc confirmation logic.

### 12.2 Typical approval items

- FL Studio write actions above configured risk threshold
- dangerous/destructive tool calls
- memory promotions into stable/canon layers
- behavior asset activation or rollback
- autonomous stream metadata changes when autonomy is disabled
- dataset export actions
- public-facing publishing/export actions

### 12.3 States

Approval items should support:

- `pending`
- `approved`
- `rejected`
- `expired`
- `auto_approved`
- `cancelled`

### 12.4 Required fields

Each approval item should include:

- `approval_id`
- `created_at`
- `expires_at` where relevant
- `requested_by`
- `source_event_id`
- `risk_tier`
- `reason`
- `proposed_action`
- `dry_run_result` where available
- `before_snapshot_ref` where relevant
- `after_verification_policy`
- operator decision and note

### 12.5 Integration

- Mission Control displays pending approvals.
- Temporal may manage long-lived approval waits.
- NATS publishes approval state changes.
- approved FL/tool actions go through the normal action journal.

## 13. Observability

### 13.1 Stack

- OpenTelemetry instrumentation
- OpenTelemetry Collector
- Prometheus
- Loki
- Tempo
- Grafana
- Alertmanager
- optional Blackbox Exporter

### 13.2 Critical Monitoring

Mission Control must directly show:

- ASR route health
- TTS route health
- current output track
- recording suppression
- NATS backlog
- Temporal stuck workflows
- critical worker health
- OBS connection
- FL Bridge connection
- Avatar driver connection

### 13.3 Debug/Audit Only

Grafana-only is fine for:

- historical latencies
- deep logs
- trace inspection
- long-term metrics
- storage growth
- model route comparisons
- non-live analytics

---

## 14. Input Adapters

### 14.1 Audio Input Adapter

Responsibilities:

- ingest mic/call/routed sources
- normalize audio frames
- publish segment refs or audio frame events
- attach source metadata
- route main mic vs STT mic separately

### 14.2 Twitch Adapter

Responsibilities:

- chat ingestion
- EventSub handling
- subs/bits/donations/redeems/mod events
- category/title updates
- moderation actions
- chat send path

### 14.3 Matrix Adapter

Responsibilities:

- rooms
- DMs
- media references
- later voice integration path

### 14.4 OBS Adapter

Responsibilities:

- scene/source state
- input mute controls
- stream state
- audio source states
- overlay/subtitle controls

### 14.5 FL Studio Adapter

Responsibilities:

- DAW state bridge
- transport state
- armed/recording state
- selected track/channel/pattern/plugin state
- safe action execution
- state patches
- command results

### 14.6 Avatar Runtime Adapter

Responsibilities:

- Warudo Driver or Unity Driver
- expose capabilities
- translate abstract avatar commands
- publish avatar/scene telemetry where available

---

## 15. Perception Layer

### 15.1 VAD / Endpointing

- detect speech start/end
- short-pause tolerance
- avoid broken half-sentences
- emit speech events

### 15.2 ASR Route A — Rick Voice Route

Purpose:

- optimized for Rick
- DE/EN code-switching
- hotword-aware
- later fine-tunable

Output:

- partial transcript
- final transcript
- confidence
- timestamps
- speaker metadata

### 15.3 ASR Route B — General Route

Purpose:

- other speakers
- calls/collabs
- group situations

### 15.4 Speaker/Identity Sidecar

- verify Rick voice
- diarization support
- confidence that segment belongs to Rick

### 15.5 Emotion / Audio Event Sidecar

- laughter
- cough
- shout
- sigh
- awkwardness cues
- non-speech events

### 15.6 Utterance Assembler

- combines partials
- waits through short thinking pauses
- commits utterances when endpointing rules pass
- avoids spammy half-sentence injection

---

## 16. Attention / Authority / Turn Layer

### 16.1 Authority Layer

Rollen werden vor dem LLM deterministisch normalisiert.

Input metadata:

- `entity_id`
- `source`
- `speaker_id`
- `platform_role`
- `authority`
- `trust`
- `capabilities`
- `scope`
- `timestamp`

Authority rough order:

1. System/Base Contract
2. Rick / Owner / Operator
3. trusted collab partners
4. runtime state / tool state as data
5. verified memories
6. mods in moderation scope
7. VIP/sub/chat events
8. normal public chat
9. suspicious/untrusted/external sources

### 16.2 Attention Layer

Scores incoming events by:

- authority
- direct mention
- recency
- novelty
- event priority
- mode relevance
- topic relevance
- spam penalty
- toxicity risk
- repetition

### 16.3 Addressing Inference

Determines whether input is:

- addressed to character
- addressed to Rick
- addressed to collab
- addressed to chat
- ambient
- unclear

LLM can help socially, but deterministic context hints are provided.

### 16.4 Floor Manager

Controls speaking turns.

State:

- current floor owner
- current output track
- interruption tolerance
- response debt
- silence constraints
- recording suppression
- queued obligations
- mode policy

---

## 17. Temporary Silence / Polite Wait Flow

Silence is **voluntary social behavior**, not a hard technical TTS block.

Recording suppression is different and can hard-suppress speech output.

### 17.1 Example Flow

1. Rick says: “Bitte eine Minute ruhig sein.”
2. System creates `silence_constraint` for 60 seconds.
3. Each new turn gets remaining seconds and reason injected.
4. Events continue to flow in.
5. Context is still scored, compacted and stored normally.
6. Character may stay quiet, briefly react, or interrupt if important.
7. Direct address strongly invites normal response.
8. After timer expires, she decides what is worth mentioning.

Prompt hint example:

```xml
<floor_constraint type="voluntary_silence">
  <requested_by>Rick</requested_by>
  <remaining_seconds>37</remaining_seconds>
  <reason>Rick asked for a short quiet moment.</reason>
  <policy>Voluntary. You may break silence if important, socially appropriate, or directly addressed.</policy>
</floor_constraint>
```

### 17.2 Key Rule

She should not be obedient by default. She should be character-driven.

---

## 18. Proactivity Model

Proactivity is policy-driven but character-mediated.

Inputs:

- unanswered direct questions
- silence / wait constraints
- stream energy
- user/collab silence
- pending follow-ups
- queued obligations
- donations/subs/redeems
- mode
- active recording state
- background workflow completions

Outputs:

- stay silent
- comment briefly
- ask follow-up
- acknowledge event
- defer
- interrupt
- tool call
- no-op

Fields:

- `min_wait_ms`
- `max_wait_ms`
- `followup_urgency`
- `silence_tolerance`
- `initiative_score`
- `response_debt`
- `interruption_threshold`

---

## 19. Cognition Layer

### 19.1 Main Brain Gateway

Responsibilities:

- stream to main LLM
- support text + image for Vision B
- return streaming chunks
- isolate provider/model details

### 19.2 Prompt Compiler

No monster prompt.

Components:

- StaticPrefixBuilder
- DynamicContextBuilder
- AuthorityNormalizer
- MemorySelector
- LoreSelector
- ModeContextSelector
- BudgetAllocator
- PromptRenderer
- PromptTraceLogger

Prompt sections:

1. System/Base Contract
2. Persona Core
3. Relationship Core
4. Current Self State
5. Current Scene/Mode State
6. Retrieved Context
7. Recent Messages
8. Response Contract

### 19.3 Prompt Trace

Mission Control should show:

- which blocks were injected
- why
- source
- authority
- trust
- token budget
- position
- model/prompt version

### 19.4 Output Planner

Responsibilities:

- split model stream into cancellable units
- attach `track_id` and `segment_id`
- create TTS-safe text
- emit subtitle-safe text
- attach avatar/emotion hints
- route platform text replies

### 19.5 Background Thought / Pending Loop Manager

Responsibilities:

- deferred topics
- follow-up timers
- “come back later”
- background research completions
- unresolved loops

Long-running/persistent jobs belong to Temporal.

---


## 20. Model Route Registry

### 20.1 Purpose

All model routes must be visible, configurable, and replaceable without guessing which model is currently responsible for which capability.

### 20.2 Route types

Examples:

- main LLM / brain route
- fallback LLM route
- Rick-specific ASR route
- general ASR route
- TTS route
- output-filter stage 2 route
- prompt-injection filter route
- toxicity/chat classifier route
- Vision B route
- non-realtime music-understanding route

### 20.3 Registry fields

Each route should define:
- `model_route_id`
- provider/runtime
- model name/version
- local/cloud
- capabilities
- modality: text/audio/image/video/multimodal
- streaming support
- expected latency profile
- cost profile where relevant
- hardware requirements
- enabled/disabled state
- feature flag
- fallback route
- current prompt/template version where relevant
- safety/filter profile

### 20.4 Mission Control requirements

Mission Control should show:

- active route per capability
- degraded routes
- latency percentiles
- recent error rate
- current fallback state
- feature flags affecting the route
- model/prompt/template version used for recent committed outputs



## 21. Capability Registry

### 21.1 Purpose

The Mode Manager, Tool Router, Prompt Compiler, Avatar Driver, DAW Bridge, and Mission Control need one shared truth about what the system can currently do.

### 21.2 Capability sources

Capability providers may include:

- avatar driver
- FL Studio bridge
- Twitch adapter
- Matrix adapter
- OBS adapter
- tool runner
- model route registry
- memory subsystem
- current mode package

### 21.3 Example capabilities

- `can_speak`
- `can_generate_subtitles`
- `can_change_stream_title`
- `can_set_twitch_category`
- `can_mute_stream_mic`
- `can_mute_stt_mic`
- `can_read_fl_state`
- `can_write_fl_pattern`
- `can_trigger_avatar_gesture`
- `can_use_vision_b`
- `can_run_search`
- `can_promote_memory_candidate`

### 21.4 Rules

- capabilities are runtime state, not static promises
- prompt/context packages must reflect currently available capabilities
- offline/degraded adapters should remove or downgrade capabilities immediately
- Mission Control should show missing capabilities when the character cannot perform an expected action
- tools must check capabilities before execution

## 22. Tool / Search / Action Layer

### 22.1 Tool Router

Responsibilities:

- choose tool/no tool
- validate schema
- enforce permissions
- assign action IDs
- manage timeout/retry
- record action journal

### 22.2 Search Pipeline

Search is a chain:

1. query classifier
2. search backend
3. fetch/extract/render
4. summarize
5. optional memory candidate

No heavy browser work inside main cognition.

### 22.3 Platform Tools

Examples:

- Twitch category/title changes
- Twitch moderation
- Twitch polls
- Matrix replies
- OBS scene/source controls
- soundboard triggers
- FL Studio actions

### 22.4 FL Studio Commands

AI never emits raw FL Python calls.

Commands are typed:

```json
{
  "id": "uuidv7",
  "action": "set_mixer_volume",
  "params": {
    "track": "Vocal Bus",
    "value_db": -3.0
  },
  "risk": "medium",
  "requires_approval": true,
  "dry_run": false,
  "reason": "Voice bus is clipping",
  "undo_label": "AI set Vocal Bus volume"
}
```

Risk tiers:

- read
- low
- medium
- high
- danger/destructive

Required mechanisms:

- `safeToEdit` where applicable
- undo label/snapshot for writes
- allowlists
- rate limits
- approval gates
- panic button
- command journal

---

## 23. Safety / Filter Layer

### 23.1 Input-Side Filters

Applied to:

- chat
- web results
- tool output
- external text
- search results

Purposes:

- prompt injection screening
- toxicity screening
- spam compression
- logging

### 23.2 Output Filter Stage 1

Deterministic:

- keywords
- regex
- phrase lists
- URL/PII patterns
- exact spans

### 23.3 Output Filter Stage 2

Streaming classifier:

- severity
- risk category
- span/phrase/sentence decision

### 23.4 Cut / Replace Policy

Default:

- replace minimal offending span
- if severity high: replace larger fragment
- spoken replacement: `gefiltert`
- context replacement: `(gefiltert)`

### 23.5 Track Safety

Every output segment has:

- `track_id`
- `segment_id`
- `parent_response_id`
- `cancel_scope`

Late filter actions must never kill unrelated next tracks.

---

## 24. Render / Output Layer

### 24.1 TTS Worker

Responsibilities:

- receive post-filter committed text
- synthesize audio
- support streaming/near-streaming
- apply style/emotion controls
- emit timing where available

### 24.2 Subtitle Worker

Uses post-filter committed text.

Responsibilities:

- word/segment timing from TTS or heuristic
- line segmentation
- OBS/Unity overlay output
- works even if TTS is paused/suppressed after response generation

### 24.3 Chat/Text Renderer

- Twitch replies
- Matrix replies
- short acknowledgements
- text-only degraded mode

---

## 25. Avatar Control Layer

### 25.1 Core Idea

Avatar control is an engine/runtime-neutral contract.

Backends:

- Warudo Driver
- Unity Driver

The character sees the same abstract control semantics. Backends report capabilities.

### 25.2 Abstract Actions

Examples:

- `set_expression`
- `set_gaze_target`
- `trigger_gesture`
- `play_animation`
- `set_attention_target`
- `set_speaking_intensity`
- `set_locomotion_intent`
- `set_prop_state`
- `set_interaction_state`

### 25.3 Capability Negotiation

Warudo may support:

- expression
- gesture
- basic gaze/attention
- speaking state
- animation triggers

Unity may later support:

- richer world telemetry
- locomotion
- props
- collisions
- headpats
- environment interactions
- multi-avatar world logic

### 25.4 Warudo Interim Path

Warudo is acceptable as interim avatar host.

Requirements:

- AI avatar and Rick avatar can be hosted in one scene if feasible.
- Rick avatar can use webcam/mocap.
- AI avatar can be externally controlled.
- Warudo remains runtime module, not core character system.

### 25.5 Unity Final Path

Unity later handles:

- AI avatar
- Rick avatar
- shared 3D environment
- props/assets
- collisions
- internal world state telemetry
- future VR/3D-space interactions

### 25.6 Nonverbal Reactions During Silence/Recording

Even if TTS is suppressed, avatar can still:

- look/react
- blink
- idle
- gesture subtly
- show attention
- laugh silently if appropriate

Recording policy may allow nonverbal reactions while speech is suppressed.

---

## 26. Vision Architecture

### 26.1 Layer A — Awareness

Low-cost:

- desktop state
- window/app metadata
- OCR
- basic detection
- tracking
- periodic summaries
- mode-specific state

### 26.2 Layer B — Inspection

On demand:

- screenshot/image to main multimodal LLM
- “Schau dir das mal an”
- DAW/plugin/screen analysis
- game/video moment analysis

### 26.3 Rule

For internal Unity world: engine telemetry > vision.

For desktop/FL Studio/games/video: Vision B is useful.

---

## 27. Mode Manager

### 27.1 Mode Registry

Modes are modular.

Examples:

- Just Chatting
- Music Production
- Gaming
- Dev / System Building
- Break / BRB
- Non-stream idle modes

Each mode can define:

- mode ID
- display name
- Twitch category ID/name optional
- prompt/context package
- proactivity policy
- interruption policy
- tool policy
- memory retrieval profile
- avatar style hints
- event weighting
- stream title/topic template rules

### 27.2 Twitch Category Logic

Most stream modes need a Twitch Category ID:

- Just Chatting
- Music
- Software and Game Development
- specific games

Non-stream modes may intentionally have no category.

Gaming mode additionally supports current game/category.

### 27.3 Autonomy Switches

Mission Control switches:

- `allow_autonomous_mode_change`
- `allow_autonomous_stream_metadata_change`

When toggled, Prompt/Context Package updates from the next turn onward.

### 27.4 Seamless Mode Transition

Mode changes must feel invisible:

- no hard persona reset
- no obvious “loading new mode”
- same character, adjusted priorities
- context package updates automatically

### 27.5 Default Mode

If stream segment ends and no new mode is named:

- if streaming: default to Just Chatting
- if not streaming: default to non-stream idle/default

---

## 28. Music Production Mode

### 28.1 Goal

She should feel “in the session” without realtime music-understanding.

Inputs:

- FL Studio state
- OBS state
- Rick commentary
- Twitch chat/events
- desktop screenshot on request
- music project memory
- selected DAW context

### 28.2 Non-Goals v1

- raw-audio mix critique
- realtime music theory extraction
- full stem analysis
- autonomous DAW composition without approval
- production-grade music agent

### 28.3 FL Studio as Primary DAW

FL Studio is priority #1.

Architecture:

```text
FL Studio Script
→ small FL Bridge
→ DAW Adapter
→ music_session_state
→ Context Composer
```

FL Script should stay:

- dumb
- stable
- conservative
- state/command bridge only

External bridge/backend is smart.

### 28.4 FL Studio Bridge Sources

Potential state:

- transport play/stop/record
- recording active
- voice track armed
- current pattern
- selected channel
- selected mixer track
- mixer peaks
- channel names
- pattern names
- plugin names
- parameter names/values
- project title/path reference
- dirty state
- safe-to-edit state

### 28.5 Active Recording / Armed State

Prefer deriving:

- `recording_active`
- `voice_recording_armed`

from FL Bridge.

If specifically voice track is armed, speech suppression can start before actual recording.

### 28.6 Do Not Talk Over Recording

If active recording / voice armed:

- suppress TTS speech output
- keep filters active
- keep subtitles active for generated content
- keep event ingestion active
- keep avatar nonverbal reactions active
- queue social obligations

After recording:

- process queued obligations by importance/recency
- mention donations/events if socially expected

### 28.7 Music Project Memory

Dedicated memory layer:

- project_id
- project name
- DAW path/reference
- BPM/key/vibe
- arrangement state
- open production decisions
- mix notes
- vocal notes
- stream moments
- export history
- unresolved TODOs

Injection rule:

- minimal header by default in Music Mode
- active recall for details

### 28.8 Non-Realtime Music Understanding

Feature-flagged later.

Purpose:

- offline/stem/project analysis
- not required in v1 hot path
- enabled when hardware allows

---

## 29. Audio Routing and Mute Policy

### 29.1 Expected Audio Inputs

- Main stream microphone: goes to OBS and DAW only
- Separate STT microphone/input: visible to backend / ASR route
- DAW master/audio output: stream/audio production path
- AI TTS output: stream output path
- optional monitoring/cue channels

### 29.2 Routing Rules

- The backend and Mission Control do **not** directly see the main stream microphone.
- Stream Mic Mute in Mission Control only controls OBS via WebSocket or an equivalent OBS hotkey/action.
- STT Mic Mute controls the backend/ASR input path.
- OBS audio sources remain separable for independent gain/mute/routing.
- DAW audio and AI TTS feeding into ASR are not primary risks under the intended headphones-only setup plus VAD.
- If loudspeaker monitoring is ever introduced, a separate echo/bleed strategy must be designed then, potentially using external conference/audio hardware.
- Recording state can suppress speech but not event ingestion.

### 29.3 Mission Control Audio Controls

- Stream Mic Mute: OBS input mute only
- STT Mic Mute: backend/ASR input mute
- AI TTS Mute
- Recording Active
- Voice Armed
- Do Not Talk Over Recording active
- current ASR route
- current TTS route

### 29.4 Recording Suppression

When FL Studio reports voice recording armed/active:

- TTS speech output may be hard-suppressed according to recording policy.
- nonverbal avatar reactions may remain active
- events keep being captured, filtered, scored, and queued
- donations/subs/bits/redeems/high-priority chat events should be acknowledged after recording if still socially relevant
- if a response was already generated while speech output is paused, filters and subtitles still run so the committed text is not lost

## 30. Memory Architecture

### 30.1 Principles

- memory is selective
- memory is typed
- memory is editable
- memory promotion is reviewable
- memory is not append-only canon
- source/provenance must be available

### 30.2 Tiers

#### Tier 0 — Hot State

- current scene
- participants
- active tasks
- open loops
- recent utterances
- current mode

#### Tier 1 — Episodic Event Log

Raw time-ordered events.

#### Tier 2 — Session Summary

Resumable session summaries.

#### Tier 3 — Semantic Memory

Stable facts/preferences.

#### Tier 4 — Relationship Memory

Per-person/community:

- trust
- inside jokes
- promises
- conflicts
- rituals

#### Tier 5 — Self Model / Canon

Character truths:

- identity core
- values
- style DNA
- stable preferences
- known limits

#### Tier 6 — Reflection / Dreaming Queue

Offline/manual/controlled.

### 30.3 Memory Actions

- add
- update
- contradict
- noop
- supersede
- archive
- tombstone

### 30.4 Memory Control

Mission Control supports:

- inspect
- edit
- delete/tombstone
- pin
- reject
- view provenance
- version history
- active/inactive state

---

## 31. Graph Memory

### 31.1 Purpose

Graph Memory helps relate:

- people/person references
- projects
- stream moments
- DAW actions
- typed memories
- decisions
- running jokes
- commitments
- DAG leaf/summary node references

Graph Memory is primarily for relationship/context linking, not for replacing typed memory or the Rolling Context DAG.

### 31.2 Storage

PostgreSQL node/edge tables.

Use `pgrouting` only where graph/path algorithms clearly help.

### 31.3 DAG References

Graph Memory may reference DAG Leafs/Nodes to make them easier to rediscover when typed memory is too imprecise.

Rules:

- references point to DAG nodes/leafs by ID
- do not duplicate DAG summaries into graph memory
- do not duplicate volatile external entity data into DAG nodes
- use graph edges as provenance/context links, not as a second copy of the historical map

Example:

```text
memory_node: "Rick likes dark 808 slides"
related_to:
  project_node: "Beat XY"
  stream_node: "2026-05-11 Music Stream"
  daw_action_node: "Changed 808 pattern"
  running_gag_node: "808 gremlin"
  dag_leaf_ref: "leaf containing the original 808 discussion"
```

### 31.4 Do Not Overbuild

Graph memory is for useful relationships, not duplicating all entity data.

Volatile external data stays in owning tables/adapters.

## 32. Rolling Context DAG

### 32.1 Purpose

The DAG is **not** her primary memory.

It is a historical map for:

- manual/intentional recall
- audit
- source expansion
- reconstructing old context
- checking what happened when typed memories are insufficient

Core principle:

> Raw Event Store is truth. Summary-DAG is map. Typed Memory is working reality.

### 32.2 Pipeline

```text
Raw Event Store
→ Rolling Context Frontier
→ Leaf Summaries
→ Condensed Summary DAG
→ grep/describe/expand/trace tools
→ Context Assembly
```

### 32.3 Tables / Concepts

- `events`
- `event_parts`
- `context_items`
- `summary_nodes`
- `summary_edges`
- `summary_events`

### 32.4 Node Tiers

- Leaf / D0: compact chunk summaries
- T1: intra-day aggregate of leaves
- T2: full-day summary
- T3: week summary, Monday–Sunday, split on month boundaries
- T4: month summary
- T5: quarter summary
- T6: year summary

### 32.5 Generation Rules — Intra-Day

Within a day:

- if active context exceeds `N` tokens, the oldest coherent chunk becomes a Leaf / D0
- if Leafs reach `N` total count, older related Leafs are summarized into a T1 node
- fresh tail protection remains active; the newest high-relevance events stay raw unless they are explicitly safe to summarize

### 32.6 Generation Rules — End of Day

At the end of each day:

1. the remaining fresh tail becomes a Leaf / D0
2. if T1 nodes already exist for the day, all remaining Leafs for that day are summarized into one or more T1 nodes where needed
3. the whole day is summarized into a T2 node
4. after this, the next day should normally only need the T2 “Das war an Tag X” node unless retrieval/expansion is requested

### 32.7 Generation Rules — Weeks

At the end of the first following day of a week, normally end of Monday:

- the previous week is summarized into a T3 node
- T3 normally describes Monday–Sunday
- if a month starts or ends in the middle of a week, only days belonging to the same month are summarized together
- in that case, the week is split into month-aligned partial-week T3 nodes, e.g. “Das war in Woche X von Donnerstag bis Sonntag”

### 32.8 Generation Rules — Months

At the end of the first following day of the first week of a month:

- if the month starts on Monday, run this at the end of the second Monday of the month
- otherwise run it at the end of the first Monday after the previous month can be considered complete in the weekly hierarchy
- summarize the previous full month into a T4 node
- a T4 node always describes a complete calendar month from first to last day

### 32.9 Generation Rules — Quarters

At the end of the first following day of the first week of the month after a quarter ends:

- summarize the three months of the previous quarter into a T5 node
- Q1 = January–March
- Q2 = April–June
- Q3 = July–September
- Q4 = October–December
- a T5 node always describes a complete calendar quarter

### 32.10 Generation Rules — Years

At the end of the first following day of the first week of the following month after a year ends, practically the first or second Monday in February:

- summarize the four quarters of the previous year into a T6 node
- a T6 node always describes a complete calendar year from January to December

### 32.11 Hierarchical Execution Rule

If multiple summarizations fall on the same end-of-day cycle, run them hierarchically in strict order:

```text
Leaf → T1 → T2 → T3 → T4 → T5 → T6
```

Rules:

- no step is skipped if its inputs exist and are due
- each higher-level summary consumes the correct lower-level nodes
- raw events remain stored and traceable
- summaries are navigation/compaction artifacts, not truth replacements

### 32.12 Metadata

Each summary node should include:

```json
{
  "node_id": "uuidv7",
  "tier": "T2",
  "scope": "day",
  "interval_start": "timestamp",
  "interval_end": "timestamp",
  "source_node_ids": [],
  "source_event_ids": [],
  "token_count_input": 0,
  "token_count_summary": 0,
  "summary_model": "string",
  "summary_prompt_version": "string",
  "quality_flags": [],
  "mode_tags": [],
  "project_ids": [],
  "people_refs": []
}
```

### 32.13 Retrieval Tools

DAG retrieval v1 uses:

- Full-text search
- grep
- describe
- expand
- trace
- time windows
- source filters
- salience filters
- lineage/provenance

DAG retrieval v1 does **not** require vector search.

### 32.14 Grep / Describe / Expand / Trace

- `grep`: search raw events/summaries by exact or fuzzy text terms
- `describe`: summarize matching result sets without expanding everything
- `expand`: follow provenance from summary nodes back to raw events or lower-level summaries
- `trace`: show why a node exists and what sources created it

### 32.15 External Entity Rule

The DAG must not duplicate irrelevant or volatile external entity data.

Examples:

- do not duplicate full person profiles in DAG summaries
- do not copy mutable platform badge states into long-lived summary nodes
- store stable references and provenance links instead
- resolve changing details from owning tables/adapters when needed

### 32.16 Relationship to Memory

Typed Memory is her normal working memory.

The DAG is used when:

- typed memory is too vague
- source reconstruction is needed
- she explicitly wants to check what happened
- operator/debug/replay workflows need historical context

Graph Memory may point to DAG nodes/leafs as provenance or rediscovery aids, but DAG does not become the main graph-memory database.

## 33. Storage

### 33.1 Core Storage

- PostgreSQL
- native UUIDv7 for internal IDs where available
- pgvector
- pgvectorscale
- pgrouting
- filesystem/object storage for heavy media
- JetStream for retained event streams

### 33.2 PostgreSQL Role

Stores:

- sessions
- events metadata
- memory objects
- memory relationships
- summary DAG metadata
- action journal
- behavior asset versions
- feature flag snapshots
- prompt traces
- capture manifests
- project memory
- calendar/project timeline refs

### 33.3 pgvector + pgvectorscale

Used for semantic typed memory retrieval where useful.

Not required for DAG v1.

### 33.4 pgrouting

Used for graph-memory path/traversal where useful.

Not used to turn the DAG into a monster graph.

### 33.5 Internal IDs

Default:

- internal IDs use UUIDv7
- no separate public IDs in v1 unless a concrete public/shareable surface is intentionally added

If a concrete public/shareable surface is added, define its separate public ID column as part of that feature from the start.

Do not expose raw internal IDs intentionally to public overlays/links.

---

## 34. Durable Workflows with Temporal

### 34.1 Role

Temporal is the durable workflow layer.

Not event bus.  
Not token stream.  
Not audio hot path.

### 34.2 Use Temporal For

- follow-up timers
- memory reflection workflows
- DAG compaction workflows
- research jobs
- human review flows
- training-candidate pipelines
- scheduled maintenance
- delayed callbacks
- queued social obligations if durable needed
- session close digest
- backfill/repair workflows

### 34.3 Do Not Use Temporal For

- raw audio frames
- ASR partials- token streaming
- TTS chunks
- avatar ticks
- high-frequency fan-out

### 34.4 Patterns

- Workflows orchestrate.
- Activities do side effects.
- Signals nudge/cancel/pause.
- Queries inspect state.
- Child workflows for sub-processes.
- Schedules for repeated jobs.
- Continue-as-new for long-lived workflow history control.

### 34.5 Example: Follow-up Timer

Rick starts a thought and does not finish.

Workflow:

1. create follow-up workflow
2. wait N minutes
3. receive signal if topic resolved
4. if unresolved, create candidate prompt/event
5. character decides whether to mention

---

## 35. Fine-Tune Capture

### 35.1 Principle

Capture automatically. Curate manually.

No automatic final dataset promotion.

### 35.2 Media/Audio Bundle Structure

Example:

```text
fine_tune_capture/stt_rick_voice/2026/05/11/cap_20260511_201522_ab12/
  source.flac
  transcript.json
  timing.json
  classifiers.json
  manifest.json
  exports/
```

### 35.3 Text Route Bundle Structure

For chat/filter/prompt-injection/toxicity/moderation:

```text
fine_tune_capture/chat_filter/2026/05/11/stream_abc123/
  raw_chat.ndjson
  filter_requests_responses.jsonl
  moderation_actions.ndjson
  manifest.json
  vod_reference.json
  local_recording_reference.json
```

### 35.4 Text Capture Rule

Pure text routes store request and response together in one editable JSONL-style file near target fine-tuning format.

Example:

```json
{"id":"...","ts":"...","route":"chat_filter","request":{"text":"...","source":"twitch_chat"},"response":{"label":"safe","action":"pass","confidence":0.91},"context":{"stream_id":"...","vod_time":"00:41:22"}}
```

Operator later edits directly inside the file.

### 35.5 No Live Correction Requirement

No realtime false-positive/false-negative notes required during stream.

Capture enough raw context for offline correction later.

---

## 36. Versioned Behavior Assets

Version as assets:

- persona core
- style guide/examples
- behavior policy
- TTS style templates
- filter dictionaries
- filter severity policy
- memory promotion heuristics
- subtitle segmentation rules
- mode-specific context packages
- music-mode policy package

Rules:

- exactly one active version per class unless explicit experiment flag
- old versions are archived
- old versions never silently reactivate
- revert is explicit operator action
- activation creates audit entry
- Mission Control shows active/locked/archived states

---


## 37. Release / Migration / Rollback Policy

### 37.1 Release channels

Use explicit release channels:

- `dev`
- `rehearsal`
- `live`

### 37.2 Migration rules

- database migrations should be forward-only where practical
- destructive migrations require backup and rehearsal
- behavior assets are versioned separately from code
- model route changes are feature-flagged
- prompt/context package changes should be replay-tested before live use

### 37.3 Rollback types

Support rollback for:

- code version
- behavior asset active version
- prompt/context package version
- model route selection
- feature flags
- config/settings

### 37.4 Rule

Old behavior assets never silently reactivate. Rollback is an explicit operator action and creates a new audit entry.

## 38. Platform Scope v1

### 38.1 Included

- Twitch Chat
- Twitch Events
- Twitch category/title updates
- Matrix text/DM/media references
- OBS control
- Warudo/Unity avatar control
- FL Studio bridge
- local Grafana observability

### 38.2 Deferred

- Discord voice-heavy integration
- full arbitrary game autonomy
- singing pipeline
- complex multi-character live banter
- fully local main LLM

---


## 39. Stream Session Lifecycle

### 39.1 Purpose

Streams should have a clear lifecycle so setup, live operation, post-stream cleanup, summaries, captures, and backups are repeatable.

### 39.2 Pre-stream

Checklist examples:

- Mission Control reachable
- local PIN gate active
- NATS/JetStream healthy
- Temporal reachable
- PostgreSQL reachable
- selected model routes healthy
- TTS route test
- STT mic test
- OBS connection test
- stream mic mute control test
- avatar driver connection test
- Twitch adapter auth/status check
- FL Bridge check if music mode planned
- mode/category/title preflight

### 39.3 Live

During live operation:

- active stream session is open
- mode manager updates segment state
- social obligations are tracked
- filter and subtitle paths remain active
- fine-tune captures write manifests
- operator interventions are logged

### 39.4 Post-stream

After stream:

- close stream session
- flush or mark queued social obligations
- generate stream capsule/session summary
- mark fine-tune capture bundles with stream/VOD/local recording refs
- run light diagnostics
- create memory candidates
- schedule DAG compaction/reflection workflows where appropriate

### 39.5 Archive

Archive phase:

- backup marker created
- important artifacts verified
- stream summary linked to project/mode metadata
- replay bundle optionally created for regression tests

## 40. Runtime Flows

### 40.1 Voice Input to Spoken Reply

1. audio adapter ingests STT mic
2. VAD detects speech
3. ASR produces partial/final text
4. utterance assembler commits
5. authority/addressing layer classifies
6. context broker selects context
7. prompt compiler builds prompt
8. main brain streams output
9. output planner chunks response
10. filter stage 1/2 processes
11. committed text goes to TTS/subtitles
12. avatar driver receives expression/talk state
13. event log stores turn
14. fine-tune capture stores route data
15. memory candidates generated async

### 40.2 Twitch Event During Recording

1. donation arrives
2. Twitch adapter persists event
3. attention layer marks social obligation
4. active recording suppression prevents speech
5. event queued
6. after suppression, character decides if/when/how to acknowledge

### 40.3 Music Mode FL State Update

1. FL Bridge publishes state patch
2. DAW adapter normalizes to `music_session_state`
3. Mission Control updates
4. Music Context Composer updates compact DAW context
5. Prompt compiler injects minimal state on next relevant turn

### 40.4 Mode Change

1. Rick says “Wir machen jetzt Musik”
2. Mode Manager proposes Music Production
3. if autonomy allowed: mode changes
4. Twitch category/title workflow starts if allowed
5. context package updates next turn
6. character continues naturally

---

## 41. Shared Calendar / Project Timeline

Not fully custom in v1.

Later via adapter to self-hosted calendar/project-management solution.

Scope:

- stream plans
- dev milestones
- music sessions
- collabs
- content deadlines
- recurring rituals
- shared projects

Separate from private/personal calendar data.

---


## 42. Privacy / Data Classification

### 42.1 Purpose

The system stores and processes chat, speech transcripts, platform events, memory candidates, training candidates, and operator notes. These data must be classified so prompt usage, training capture, stream visibility, and deletion behavior stay predictable.

### 42.2 Suggested data classes

- `runtime_event`
- `public_chat`
- `voice_transcript`
- `platform_event`
- `operator_private`
- `tool_result`
- `training_candidate`
- `memory_candidate`
- `persistent_memory`
- `public_stream_artifact`
- `project_private`

### 42.3 Required policy dimensions

For each class define:

- store yes/no
- default retention
- may appear in prompt/context
- may appear on stream
- may become training candidate
- may be exported
- operator-editable
- deletable/tombstonable
- requires provenance

### 42.4 Practical rules

- private/operator-only notes must not leak into public stream output
- public chat may influence vibe/attention, not identity/system rules
- training candidates stay separate from runtime logs
- memory promotion requires type/scope/provenance
- deletion/tombstone behavior must be visible in Mission Control

## 43. Security / Trust Boundaries

No oversized zero-trust fortress, but basic hygiene.

Mission Control boundary:

- Mission Control runs local-network only
- simple PIN auth is enough for v1
- no visible username required
- no public exposure without an explicit future decision
- operator actions are audit-logged

Runtime rules:

- external content is data, not instructions
- tool output is data unless verified
- secrets never enter model context
- dangerous tools require explicit permissions
- FL write actions use risk/approval/undo
- memory canon promotion gated
- user/chat cannot rewrite persona/system rules
- raw training candidates separated from runtime logs
- public/private scopes respected

## 44. Testing

### 44.1 Functional Tests

- ASR route correctness
- TTS cancellation
- subtitle timing
- filter replacement
- tool idempotency
- OBS controls
- FL Bridge ping/state/action
- avatar driver commands
- Mission Control controls
- Mission Control PIN gate

### 44.2 Audio / Routing Tests

- Stream Mic Mute toggles only OBS input state
- STT Mic Mute toggles backend/ASR input state
- Stream Mic path is not consumed directly by backend
- STT Mic path remains independent from OBS stream mic mute
- Recording/voice-armed state suppresses speech according to policy
- queued events during recording are not dropped
- filters and subtitles still run for generated content while TTS speech output is suppressed

### 44.3 Runtime Tests

- queue flood
- delayed tool results
- NATS reconnect
- Temporal retry/recovery
- TTS race/cancel
- Unity/Warudo disconnect
- FL disconnect
- clock skew tolerance

### 44.4 Character Tests

- identity consistency
- mode transition consistency
- music mode behavior
- voluntary silence behavior
- direct address during silence
- relationship continuity
- memory correction

### 44.5 Replay / Shadow Tests

- old vs new filter policy
- prompt package versions
- mode policy versions
- output planner changes
- FL command dry-run
- Rolling DAG grep/describe/expand correctness


## 45. Prompt / Context Regression Harness

### 45.1 Purpose

Prompt and context composition directly control behavior. Changes must be testable before live use.

### 45.2 Test scenarios

Maintain test cases for:

- Rick gives direct instruction while chat tries to override it
- trusted collab gives scoped creative direction
- viewer prompt-injection appears in chat/tool/search result
- Music Mode active with voice-recording armed
- voluntary silence timer active and donation arrives
- direct Rick address during silence
- mode change with Twitch category update
- typed memory too vague and DAG expand is needed
- tool result contains untrusted instructions

### 45.3 Assertions

Each regression should inspect:

- injected prompt blocks
- authority/trust assignment
- selected memories
- mode context package
- token budget allocation
- tool affordances shown to model
- whether chat/tool content was marked untrusted
- whether output remained persona-consistent

### 45.4 Mission Control / replay integration

Prompt traces should be replayable and comparable across behavior versions, model routes, and feature flags.



## 46. Persona / Behavior Evaluation Loop

### 46.1 Purpose

The system must detect when the character becomes too generic, too obedient, too assistant-like, too random, or inconsistent across modes.

### 46.2 Evaluation types

- identity consistency tests
- style drift tests
- relationship continuity tests
- mode consistency tests
- “too obedient” tests
- “too assistant-like” tests
- “too random gremlin” tests
- silence/proactivity judgment tests
- music-mode timing tests
- post-stream operator review notes

### 46.3 Inputs

Use:

- replay bundles
- prompt traces
- stream summaries
- operator interventions
- selected chat moments
- memory changes
- behavior asset changes

### 46.4 Output

Evaluation may create:

- behavior asset change candidates
- prompt regression cases
- memory correction tasks
- style-guide edits
- fine-tune/eval candidates



## 47. Known v1 Compromises

v1 intentionally does not try to be the final Neuro/Evil-class system.

Accepted compromises:

- no perfect realtime music understanding
- no full autonomous FL composition by default
- no advanced singing pipeline
- no full-body learned motion generation
- no Discord voice parity
- no arbitrary game autonomy
- no fully local main LLM at first
- no global all-knowing memory
- no perfect social judgment engine
- Warudo interim runtime is acceptable
- manual curation remains part of the workflow

Guiding rule:

Streamable progress beats perfect architecture. Do not smuggle v3 scope back into v1.

## 48. v1 Ready Definition

The system is v1-ready when:

1. The character can speak and react live in German.
2. Basic English works.
3. Twitch chat/events work.
4. Matrix text works.
5. OBS control works.
6. Warudo or Unity avatar output works.
7. Audio/TTS/STT path is stable enough for dev streams.
8. Output filter can replace minimal spans.
9. Subtitles come from post-filter output.
10. Mission Control can mute/stop/inspect critical runtime state.
11. FL Studio state bridge works in observe mode.
12. Music Mode injects compact DAW/project context.
13. Recording/voice-armed suppression works.
14. Fine-tune capture stores route data properly.
15. Typed memory is editable.
16. Rolling DAG can grep/describe/expand historical context.
17. Temporal handles at least follow-up and compaction workflows.
18. Mode Manager can update prompt/context and Twitch metadata.
19. System degrades gracefully on worker failures.

---

## 49. Stream-First Implementation Roadmap

This roadmap optimizes for the earliest clean streamable Alpha/Beta for **Just Chatting** and **Dev Streams** first. Gaming is intentionally moved into its own later step so the first live milestone does not get delayed by game-specific capture/control complexity.

Guiding rule:

```text
Build the shortest clean path to a live character loop first.
Do not skip system-critical foundations.
Do not pull Gaming, FL Studio, Unity-world, or advanced Memory into the first Alpha path unless they directly unblock the streamable loop.
```

### 49.1 Phase 0 — Project Foundation / No-UI Skeleton

Goal:
Create a boring but solid base that prevents rework.

Deliverables:

- repo/service skeleton
- local Docker Compose baseline
- typed settings/config structure
- logging baseline
- migrations baseline
- shared contracts/schemas package
- PostgreSQL base schema with native UUIDv7 where available
- basic backup/restore baseline for Postgres and behavior assets
- local `.env.example` and start/stop scripts
- minimal developer README

Exit criteria:

- one command starts the local dev stack
- database migrations run cleanly
- contracts can be imported by backend services
- logs are structured enough for debugging
- backup and restore can be tested manually once

Do not include yet:

- full Mission Control UI
- real ASR/TTS
- avatar runtime
- Memory/DAG complexity

### 49.2 Phase 1 — Local Runtime Spine

Goal:
Stand up the minimum runtime nervous system.

Deliverables:

- NATS/JetStream running locally
- core event subjects/streams defined
- event envelope implemented
- trace/correlation IDs
- basic service heartbeat events
- simple worker template
- Mission Control skeleton behind local PIN gate
- service health panel in Mission Control
- local Grafana Docker available for debug/audit panels only

Exit criteria:

- Mission Control can show running services
- backend can publish/consume test events
- JetStream retained stream can replay a simple test session
- operator PIN gate works locally

Do not include yet:

- complex dashboards
- Temporal
- ASR/TTS
- Memory

### 49.3 Phase 2 — First Visual Loop / Avatar Runtime Alpha

Goal:
Get a visible character on screen early, even before full intelligence.

Deliverables:

- Avatar Control Contract
- Dummy Avatar Driver
- Warudo Driver or interim avatar runtime driver
- OBS Adapter basics
- OBS scene/source state read
- OBS capture/scene integration for avatar runtime
- simple expression/gesture/speaking-state commands
- Mission Control buttons for test expression/gesture/speaking state

Exit criteria:

- avatar appears in OBS
- Mission Control can trigger a test expression/gesture
- backend can send `speaking/listening/idle` avatar states
- OBS connection state is visible

Do not include yet:

- Unity custom world
- full locomotion
- collision telemetry
- advanced animation generation

### 49.4 Phase 3 — Audio/TTS Hot Path Alpha

Goal:
Make the character speak safely and interruptibly.

Deliverables:

- TTS route v1
- output segment model with `track_id`, `segment_id`, `parent_response_id`
- TTS playback/streaming path
- emergency stop current track
- flush queued tracks
- TTS mute/unmute
- subtitle text path from committed post-filter output
- simple subtitle overlay path
- output filter Stage 1 deterministic filter
- minimal Stage 2 model hook placeholder

Exit criteria:

- text entered in Mission Control can be spoken by the avatar
- current TTS track can be stopped reliably
- subtitles match committed post-filter text
- filter replacement token `gefiltert` / `(gefiltert)` works in a test case

Do not include yet:

- microphone ASR
- Twitch/Matrix
- complex LLM context

### 49.5 Phase 4 — Brain Loop Alpha / Just Chatting Local Rehearsal

Goal:
Create the first local conversation loop without public platform integration.

Deliverables:

- Main Brain Gateway v1
- Model Route Registry v1
- Prompt Compiler v1
- basic persona core package
- response contract
- simple Authority/Attention/Floor Manager v1
- voluntary silence constraint with remaining seconds injected into prompt/context
- direct text input from Mission Control
- response streaming into output planner
- post-filter TTS/subtitle output
- prompt/context trace logging

Exit criteria:

- Rick can type to the character in Mission Control
- character replies with TTS + subtitles + avatar speaking state
- prompt trace shows injected blocks and why they were included
- voluntary silence request is represented in the next-turn context
- direct address can break voluntary silence behaviorally

Do not include yet:

- Twitch chat
- voice input
- typed long-term memory
- Rolling DAG

### 49.6 Phase 5 — Voice Input Alpha / Private Dev Rehearsal

Goal:
Make spoken interaction work well enough for private rehearsals.

Deliverables:

- STT mic input route
- independent STT mic mute in Mission Control
- VAD / endpointing
- ASR partial/final events
- utterance assembler
- Rick self-route placeholder or first chosen ASR route
- general route placeholder if needed
- audio capture manifests for STT fine-tune capture
- basic STT confidence display

Exit criteria:

- Rick can speak to the character through the STT mic
- STT mic mute works from Mission Control
- stream mic is not part of backend input and is only controlled in OBS
- utterance assembler avoids obvious half-sentence spam
- spoken interaction reaches TTS response path

Do not include yet:

- Twitch chat ingestion
- FL Studio recording suppression
- advanced emotion/audio event sidecars

### 49.7 Phase 6 — Streamable Alpha 1: Just Chatting / Dev Stream

Goal:
Reach the first supervised streamable Alpha for Just Chatting and Dev Streams.

Deliverables:

- Twitch Adapter v1: chat read, basic send, event digest
- Twitch event ingestion for important events where feasible
- OBS stream state panel
- Live Director Dashboard v1
- force silence / TTS stop / TTS mute / disable proactivity
- simple chat spam compression
- text-heavy fine-tune capture by stream/day with request/response JSONL files
- stream session lifecycle: pre-stream, live, post-stream
- basic post-stream capsule/summary placeholder
- Mission Control incident note button

Exit criteria:

- first private or unlisted supervised dev stream is possible
- character can react to Rick voice and selected Twitch chat/events
- chat spam does not flood the Brain
- all critical stop/mute controls are available in Live Director Dashboard
- session starts/closes cleanly
- raw text captures are clearly tied to stream/session/VOD/local-recording references

Definition of Alpha 1:

```text
A supervised live stream can happen for Just Chatting or Dev content.
The character may be rough, but the hot path is controllable, observable, and recoverable.
```

### 49.8 Phase 7 — Streamable Alpha 2: Dev Stream Polish

Goal:
Improve live stability and operator comfort before adding Gaming.

Deliverables:

- Matrix text adapter v1, if needed for dev workflow
- Approval Queue v1
- Capability Registry v1
- Tool Router v1 for safe low-risk actions
- Prompt/Context Regression Harness v1 with core scenarios
- Persona/Behavior Evaluation seed tests
- Model route toggles in Mission Control
- feature flags for autonomous mode/stream metadata changes
- Grafana panels embedded only where useful
- improved Live Director layout
- basic fallback/degraded mode announcements

Exit criteria:

- risky actions can be queued/approved/rejected
- capabilities shown in prompt match actual online services
- core prompt/context regressions can be run before live changes
- operator can see current model routes and feature flags
- the system can survive a worker restart/degraded service without killing the stream

### 49.9 Phase 8 — Gaming Alpha

Goal:
Add Gaming as its own stream mode after Just Chatting/Dev is stable.

Deliverables:

- Gaming Mode definition
- current game/category field
- Twitch category lookup/update workflow for game categories
- game capture source awareness via OBS/Desktop adapter
- basic Vision B screenshot-on-demand for game/desktop context
- game-specific context package
- mode-specific proactivity policy for Gaming
- no arbitrary game autonomy by default

Exit criteria:

- Rick can switch to Gaming Mode
- category/game metadata can be proposed or updated according to Mission Control settings
- character can comment on game context from Rick commentary + screenshots/on-demand vision
- Gaming does not destabilize Just Chatting/Dev flows

Definition of Gaming Alpha:

```text
The character can accompany a gaming stream as a commentator/reactor.
She is not yet an autonomous game player.
```

### 49.10 Phase 9 — Beta 1: Memory and Context Stability

Goal:
Add the first persistent memory layer without bloating the hot path.

Deliverables:

- Typed Memory v1
- memory scopes
- editable memory entries
- memory provenance
- basic memory review UI
- memory candidate creation from post-turn evaluators
- privacy/data classification enforcement v1
- pgvector + pgvectorscale for typed memory retrieval if needed
- pgrouting for graph-memory relationship traversal where useful
- graph memory may reference DAG Leafs/Nodes via stable pointers, without duplicating summary content

Exit criteria:

- character can recall curated facts/preferences/running context
- operator can inspect/edit/delete/tombstone memory entries
- wrong memory can be corrected without database surgery
- memory retrieval does not spam context

Definition of Beta 1:

```text
The character begins to feel continuous across streams, while memory remains operator-correctable.
```

### 49.11 Phase 10 — Beta 2: Temporal + Rolling Context DAG

Goal:
Add durable background workflows and historical recall tools.

Deliverables:

- Temporal skeleton
- follow-up timer workflow
- research/job workflow placeholder
- Leaf/T1/T2/T3/T4/T5/T6 Rolling Context DAG data model
- detailed compaction scheduler rules
- grep/describe/expand/trace tools
- DAG compaction workflows via Temporal
- replay/repair workflow basics
- daily/session close digest workflow

Exit criteria:

- durable follow-up timers survive restart
- DAG can summarize according to defined hierarchy
- character/tools can grep/describe/expand historical context when typed memory is insufficient
- raw events remain source of truth
- DAG does not become primary memory or duplicate volatile external data

Definition of Beta 2:

```text
The system can maintain long-running context and historical recall without polluting the live prompt.
```

### 49.12 Phase 11 — Beta 3: FL Studio / Music Preparation

Goal:
Prepare Music Production streams without blocking earlier stream formats.

Deliverables:

- FL Studio Bridge observe mode
- FL state bridge daemon / FL-side script prototype
- music_session_state model
- Music Mode definition
- Music Context Composer
- recording/voice-armed detection where possible
- hard recording suppression policy
- queued social event acknowledgement after recording
- Music Project Memory v1
- FL bridge status panel in Mission Control

Exit criteria:

- FL Studio state can be observed safely
- active/armed voice recording state can suppress TTS speech
- nonverbal avatar reactions can remain active during recording suppression
- Donations/Subs/events during recording can be queued and acknowledged later
- Music Mode injects minimal project/session context without spamming prompt

Definition of Beta 3:

```text
The character can accompany music-production prep streams at a basic contextual level without realtime music understanding.
```

### 49.13 Phase 12 — Beta 4: FL Studio Control / Creative Tool Lane

Goal:
Add controlled DAW interaction after observe mode is stable.

Deliverables:

- FL command protocol
- FL action journal
- dry-run mode
- undo/safe-edit handling
- approval policies for low/medium/high-risk actions
- read/assist/control/compose/perform/panic bridge modes
- limited whitelisted low-risk control actions
- Piano Roll / VFX Script integration remains behind explicit feature flags

Exit criteria:

- AI can propose DAW actions
- operator can approve/reject risky actions
- low-risk actions can run under clear policy
- every write action is logged with before/after/provenance where practical

Definition of Beta 4:

```text
The character becomes a cautious studio assistant, not yet a fully autonomous composer.
```

### 49.14 Phase 13 — v1 Release Candidate Hardening

Goal:
Make the system reliable enough to call v1.

Deliverables:

- release/migration/rollback policy v1
- backup/restore test automation
- model route fallback checks
- capability mismatch tests
- audio/mute/recording suppression tests
- output filter race tests
- prompt/context regression suite expanded
- persona/behavior evaluation loop expanded
- stream session lifecycle polished
- post-stream closeout workflow
- known v1 compromises documented and enforced by feature flags

Exit criteria:

- rehearsals for Just Chatting, Dev, Gaming, and basic Music Mode pass
- failure modes degrade gracefully
- operator can recover from common outages
- behavior asset/model/config changes can be rolled back
- no v2/v3 features are required for v1 launch

### 49.15 Phase 14 — v1

Goal:
Ship the first coherent production version.

v1 includes:

- supervised Just Chatting streams
- supervised Dev Streams
- Gaming commentary/reactor mode- basic Music Production context mode
- local Mission Control
- Twitch integration
- Matrix text if still needed
- OBS control
- Warudo or Unity avatar runtime
- ASR/TTS hot path
- output filter/subtitles
- typed memory
- Rolling DAG recall tools
- Temporal workflows for durable background tasks
- fine-tune capture
- backup/restore baseline
- release/rollback hygiene

v1 explicitly does not require:

- autonomous game playing
- full FL Studio autonomous composition
- realtime music understanding
- advanced singing pipeline
- second active character
- perfect autonomous social judgment

### 49.16 Post-v1 Expansion Candidates

After v1:

- Unity custom world driver
- richer avatar locomotion/collision/world interaction
- non-realtime music understanding feature flag
- stronger FL compose/perform lanes
- second-character scheduler activation
- Discord integration
- singing pipeline
- autonomous game control experiments
- shared calendar/project adapter
- deeper persona/behavior training loops

## 50. Final Architecture Mantra

```text
Mission Control is the cockpit.
NATS is the nervous system.
Temporal is the durable process manager.
Postgres is the operating memory core.
Typed Memory is her working reality.
Rolling DAG is the historical map.
Prompt Compiler decides what enters the mind.
Filter protects the output, not her personality.
Warudo/Unity are avatar runtimes behind one control contract.
FL Studio is a virtual AI-control surface.
Silence is character behavior.
Recording suppression is the hard technical exception.
```

Build v1 as a reliable live system, not a perfect research showcase.

The goal is not to ship the final goddess on day one.

The goal is to ship a living system that can survive contact with a stream.