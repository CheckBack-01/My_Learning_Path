
# Phase 4 — Univac 1108 (Evasion, Persistence & C2)

**Scope.** Phase 4 consolidates **evasion, persistence, and C2** in an **isolated lab environment**, focusing on loader/implant engineering, telemetry-aware design, and controlled deployments. All work is educational and governed by **OPSEC/Legal**.

**Methodology.** Each block concludes with **PBR** (reproducible lab) + **PAD** (Practical Aptitude Drill: a block-level integrated mission with evidence and replication steps).

**Phase-level outcomes.**
• **OPSEC playbook** and lab checklist • **Implant/loader** with decoupled configuration, encrypted channel, and timing control • **Persistence** on Windows/Linux with **safe rollback** • Functional **lab C2** (server + client) with logging and metrics • **Evasion** report focused on detection surfaces and artifact-reduction measures • **Reproducible infrastructure** (scripts/containers) • **F4 Capstone**: end-to-end chain with controlled deployment and evidence package.

---

## How Phase 4 is organized

**Nomenclature.** Blocks use codes like `0B04`, where `X` is the zero-based block index and `YY` is the number of stacks within that block (if applicable).

**Blocks in Univac 1108**

### `0B03` — Pre-flight bridge F3→F4 (readiness, OPSEC & snapshots)

**Goal.** Ensure technical and operational continuity before evasion/persistence/C2.
**Highlights.** **Freeze F3** (stable versions, tags, clean snapshots); lab assessment and network isolation; **threats and assumptions**; logbook template; signed **OPSEC/Legal** checklist.
**PBR examples.** (1) Verified, documented snapshot. (2) **Environment validation** script (network, DNS sinkhole, logs). (3) **Logbook** initialized with a minimal structure.
**PAD evidence.** Readiness report with risks, mitigations, and rollback steps.

### `1B04` — Loader & Implant Engineering (fundamentals)

**Goal.** Design a **lab loader/implant** with external configuration and an encrypted channel.
**Highlights.** Staged vs stageless, decoupled configuration, **encryption** and message authentication, timing (beacon/jitter), task handling, minimal logs; error hygiene and stability. Non-ethical offensive techniques outside the lab are out of scope.
**PBR examples.** (1) Loader that applies config (`endpoint`, key, timers). (2) Implant executing **benign tasks** (echo, list directories) and recording evidence. (3) Stability tests and resource cleanup.
**PAD evidence.** Architecture diagram, state management, and message protocol.

### `EX0B01` — Express F4: Infrastructure & reproducible deployment

**Goal.** Prepare **reproducible infrastructure** for a lab C2.
**Highlights.** Containers and basic orchestration; lab TLS; key rotation; deployment artifacts; `evidence/` template and `Makefile`/scripts.
**Deliverable.** `infra/` folder with orchestration, lab certificates, startup/teardown scripts; quick reproduction guide.

### `2B04` — Persistence with safe rollback (Windows/Linux)

**Goal.** Implement **lab persistence methods** with guaranteed **rollback**.
**Highlights.** Windows: scheduled tasks, lab services, controlled user paths; Linux: lab systemd units, cron in isolated environments; **audit** and logging requirements; uninstall and cleanup testing.
**PBR examples.** (1) Windows lab persistence with **install/uninstall** script. (2) Linux lab persistence with state verification. (3) High-level event logging for audit.
**PAD evidence.** Proof of install, start, stop, and **rollback** with no residue.

### `3B04` — Evasion and detection surfaces (telemetry first)

**Goal.** Identify **detection surfaces** and reduce implant/loader artifacts under lab conditions.
**Highlights.** Artifact modeling: files, keys, processes, network, and memory; minimal **telemetry** (high-level ETW, system logs) to observe effects; **build hardening**, neutral names/paths, footprint minimization; **defensive** and educational focus.
**PBR examples.** (1) Artifact matrix with proposed controls. (2) Footprint-modified build compared to baseline. (3) Observability report with simple metrics.
**PAD evidence.** Impact report with before/after and limits.

### `4B03` — Lab C2: channel and server design

**Goal.** Build a **lab C2** with an encrypted channel and basic metrics.
**Highlights.** Common lab protocols (HTTPS/WebSocket/DNS tunneling constrained to an isolated network), work queues, peer authentication, retries and backoff, task/result logging; operational security in the lab.
**PBR examples.** (1) **Lab C2 server** with minimal endpoints. (2) **Client/implant** that checks in and executes benign tasks. (3) Simple metrics dashboard (tasks, latency, status).
**PAD evidence.** Protocol documentation, message formats, and resilience testing under failure scenarios.

### `5B03` — Packaging, deployment, and change control

**Goal.** Package and deploy artifacts in the lab with **traceability** and version control.
**Highlights.** Semantic versioning, signing of **lab artifacts**, build catalog, internal distribution channel, canary testing and rollback; publish/retire checklist.
**PBR examples.** (1) Labeled, signed build pipeline for the lab. (2) Publication to an internal repository. (3) Documented **rollback** flow.
**PAD evidence.** Evidence of a complete release→rollback cycle with logbook entries.

### `6B02` — F4-CAP: Full chain (loader/implant + persistence + C2)

**Goal.** Integrate capabilities: loader/implant, persistence with safe rollback, and lab C2; defend the solution in a technical presentation.
**Highlights.** Client/server integration, controlled deployment, stress tests, footprint measurement; **hardening** and countermeasures; evidence package with timings, harness, hashsets, and a short video.
**Deliverable.** `capstone-f4/` repo with code, scripts, and `infra/`; reproducible `README.md`; evidence (logs, screenshots, hashsets) and technical defense.

---

## What you’ll learn (skills & mindset)

* Loader/implant engineering with decoupled configuration and an encrypted channel.
* **Reversible** persistence on Windows/Linux oriented to auditability.
* **Lab C2** design with authentication and metrics.
* Evasion focused on **artifact reduction** and observability.
* Packaging, deployment, and rollback with traceability.
* Reproducible documentation and OPSEC/Legal discipline.

---

## Outcomes & success criteria

* **OPSEC playbook** and Phase 4 readiness checklist.
* Stable **implant/loader** with external config and channel encryption.
* **Persistence** in the lab with verified install, start, and **rollback**.
* Functional **C2** with task logging and metrics.
* **Evasion** report based on detection surfaces and footprint changes.
* **Reproducible infrastructure** for deployment and change control.
* **F4 Capstone** integrated and defended technically.
* Phase-level grading: **A** = complete PBR/PAD; stable implant/loader and C2; reversible persistence; clear documentation. **B** = ≥80% with items to polish; **C** = ≥60% with partial reproducibility; **Redo** = <60% or deficient ethical scope.

---

## PBR & PAD — how we evaluate

* **PBR (Proof-of-Bounty-Readiness).** Reproducible lab with explicit objectives, verifiable steps, and artifacts (code, logs, screenshots, hashsets).
* **PAD (Practical Aptitude Drill).** Block-level integrated mission; evaluative, with risks/limitations and **reproducible** in your lab.

> Each block closes with **PBR + PAD** and a minimal evidence package.
