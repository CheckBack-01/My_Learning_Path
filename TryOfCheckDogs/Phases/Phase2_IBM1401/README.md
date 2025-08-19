
# Phase 2 — IBM1401 (Applied Analysis & RCE)

**Scope**
Phase 2 consolidates **applied reversing** and builds your **first userland execution paths**. You’ll analyze real binaries (static/dynamic), unpack simple layers, and develop in-memory loaders that stage benign payloads using classic injection techniques—while accounting for modern mitigations (DEP/ASLR/CFG). This phase sets up the bridge into Initial Access (8A), Blue validation (8B), and later evasion work.&#x20;

---

## Methodology

* **PBR — Proof-of-Bounty-Readiness:** reproducible labs with clear goals, pinned tooling, and minimal evidence (logs, hashes, screenshots).
* **PAD — Practical Aptitude Drill:** a **block-integrated, multi-technique mission** that evaluates applied proficiency across that block’s stacks (one PAD per block).
* **OPSEC/Legal:** lab-only, VMs, benign payloads, snapshots/rollback; no third-party targets.

---

## Phase-level outcomes

By the end of IBM1401 you will have:

* A **reversing report** for a real (lightly obfuscated) binary and a **reproducible unpack**.&#x20;
* A usable **PE parser** and small analysis utilities.&#x20;
* A **userland loader** offering **≥2 execution techniques** (e.g., CRT+LoadLibrary, APC).&#x20;
* An **intro process-hollowing** PoC (lab only).&#x20;
* Clean documentation/evidence habits suitable for Bug Bounty.&#x20;

---

## How Phase 2 is organized

* **Nomenclature:** blocks use `XBYY` (e.g., `0B04`) → `X` = block index from 0; `YY` = number of stacks in the block.
* **Blocks & flow:**

  1. `0B04` → Reversing pipeline & basic unpack
  2. `1B04` → PE internals & in-memory loaders
  3. `2B04` → Userland execution techniques & mitigations
     *(Express)* `EX0B01` → Automation & harness
* **Bridge into operations:** after `2B04`, insert **8A (Initial Access)** and **8B (Minimal Blue Track)** before deeper evasion/obfuscation.&#x20;

---

## Blocks in IBM1401

### `0B04` — Applied Reversing I: tooling, methodology & basic unpacking

**Stacks (high-level):** static analysis (strings/CFG/cc), dynamic analysis (x64dbg/WinDbg), trivial anti-analysis & bypass, single-layer unpack (e.g., UPX) + minimal IAT fix, Python support scripting.
**Core PBRs:** reversing report; manual unpack with clean dump + IAT; string/config decoder with tests.
**PAD:** end-to-end drill demonstrating the pipeline on a fresh sample (controlled).&#x20;

### `1B04` — Deep PE, Windows API & in-memory loaders

**Stacks:** PE headers/sections/imports/relocs/TLS; process/thread/memory APIs; minimal local shellcode loader; **intro manual mapping** of a benign DLL; inspection/validation (PH, PE-sieve).
**Core PBRs:** PE parser; local loader with robust error handling; minimal DLL manual-map + exported function call.
**PAD:** integrated loader mission with diagrams, safety notes, tests.&#x20;

### `2B04` — Userland execution paths & modern mitigations

**Stacks:** CRT+LoadLibrary; APC (incl. early-bird); **intro process hollowing**; PPID spoofing & creation flags (lab); light obfuscation (API hashing, string hiding); mitigations (DEP/ASLR/CFG) & detection surfaces; syscall intro (no deep unhooking yet).
**Core PBRs:** multi-mode loader (CLI-selectable techniques); hollowing PoC with safe rollback; artifact/telemetry comparison across techniques.
**PAD:** comparative mission documenting mitigations, artifacts, and next-step improvements (for 8A/8B/Phase 3).&#x20;

### `EX0B01` — Express Module F2: automation & auxiliary tooling

**Focus:** parsers/extractors (PE/ELF); loader test harness (I/O, logs, timers); reproducible test datasets.
**Output:** versioned `tools/` with docs and basic tests.&#x20;

---

## What you’ll learn — capabilities & mindset

* **Analyst’s pipeline:** know when to go static vs dynamic, how to pivot between them, and how to script away repetition.
* **Binary literacy:** read PE structures confidently; reason about imports, relocations, and TLS effects on loader behavior.
* **In-memory execution:** build loaders that are reliable, observable, and reversible in lab.
* **Mitigation awareness:** measure the impact of DEP/ASLR/CFG and manage handle/process hygiene.
* **Evidence discipline:** produce clean, reproducible repos that a third party can re-run without guesswork.

---

## Result & success criteria

* **Technical**:

  * Reproducible unpack of a packed sample; PE parser that passes basic integrity checks.
  * Loader executing benign payloads via **≥2 techniques**; **intro hollowing** PoC without crashes.
* **Documentation**:

  * Clear PADs (block-integrated missions) with diagrams, method, risks, and “how-to-reproduce”.
* **Quality bar (rubric)**:

  * **A:** reversing report + clean unpack; usable parser; loader ≥2 techniques; stable hollowing PoC; fully reproducible docs.
  * **B:** ≥80% PBR/PAD; one unstable technique or partial parser; docs sufficient.
  * **C:** ≥60% PBR/PAD; partial reproducibility.
  * **Redo:** <60% or severe instability in loaders/injection.&#x20;

---

## PBR & PAD (how they work here)

* **PBR:** small, targeted labs with pinned versions, `ENVINFO.md`, `SHA256SUMS.txt`, and scripted runs (`make lab-setup && make run`).
* **PAD (current definition):** **Practical Aptitude Drill** — a **single, integrated mission per block** that exercises multiple stacks/techniques from that block and evaluates applied proficiency with evidence and rollback.
  
---

## Ethics & scope

* **Lab-only** (VMs, NAT outbound, benign payloads).
* **No** testing against third-party systems without written authorization.
* **All** artifacts must be reversible with snapshots/rollback.
* **No** operational malware; educational PoCs only.
