
# Phase 3 — Intel 4004 (Userland Internals & Exploitation)

**Syllabus & Schedule (Quarters · Blocks · Stacks)**

**Coverage:** 2026-08-01 → \~2028-07-31
**Cadence:** \~30 h/week (5 h/day, Mon–Sat)
**Methodology:** **PBR** (reproducible labs) + **PAD** (*Practical Aptitude Drill*: block-integrated mission) · Lab-only (OPSEC/Legal)
**Global Outcomes (F3):** reproducible map of **process internals** (PEB/TEB, modules, heaps, regions), **educational exploit** with **basic ROP** and mitigation analysis, **Userland Exploitation II** (applied info leak + ROP/JOP), **heap exploitation** (LFH vs glibc) in lab, foundations of **kernel/drivers** with instructional **local elevation**, and **F3-CAP**: **userland → SYSTEM** chain in a controlled environment, plus a ready-to-use **bug bounty playbook**.

---

## Quarter Map (high level)

* **Q4 (2026-08-01 → 2026-11-30):** `F3-B1` Process and Memory Internals (userland) · `F3-B2` Userland Exploitation I (basic ROP) · **EX:** Bug Bounty Prep

  > Note: **TOCD pause** 2026-09-14 → 2027-08-02 (Bug Bounty + University; Backlogs 6–8 h/wk)

* **Q7 (2027-08-03 → 2027-11-30):** `F3-B3` Advanced Windows Internals (MM/OBJ/ETW/APC)

* **Q8 (2027-12-01 → 2028-03-31):** `F3-B4` Userland Exploitation II (info leak + ROP/JOP) · `F3-B5` Heap Exploitation (LFH vs glibc)

* **Q9 (2028-04-01 → 2028-07-31):** `F3-B6` Kernel and Driver Fundamentals (Windows) + local elevation · `F3-CAP` Userland → SYSTEM chain (Phase 3 closure)

---

## Q4 — Detailed Schedule (start to 2026-09-14)

### `F3-B1` Process and Memory Internals (3 weeks · \~90 h)

**Goal:** understand process/thread anatomy: **PEB/TEB**, loaded modules, memory regions, heaps, and lifecycles; practice inspection with debuggers and utilities.

| Stack                     | Topic Cluster (examples)                                      | Est. Hours | Key Tools                             | Assignment (PBR) · Due                                           |
| ------------------------- | ------------------------------------------------------------- | ---------: | ------------------------------------- | ---------------------------------------------------------------- |
| **Tooling & baseline**    | WinDbg/x64dbg setup, symbols, Process Hacker, VMMap/`procmap` |        15h | WinDbg, x64dbg, Process Hacker, VMMap | —                                                                |
| **PEB/TEB & context**     | accessing PEB/TEB, key fields, thread/context snapshots       |        18h | WinDbg, Ghidra                        | **PBR-F3-B1-1**: PEB/TEB map + evidence · **Due:** 2026-08-16    |
| **Modules & IAT**         | module enumeration, imports/exports, base addresses           |        18h | PE-bear, Ghidra                       | **PBR-F3-B1-2**: Module inventory + hashes · **Due:** 2026-08-23 |
| **Regions & heaps**       | high-level VADs, permissions, reserve/commit, process heaps   |        18h | VMMap/`procmap`                       | **PBR-F3-B1-3**: Regions/heaps report · **Due:** 2026-08-30      |
| **Support scripting**     | Python helpers for enumeration/logs, JSON/CSV artifacts       |        12h | Python                                | —                                                                |
| **Validation & evidence** | reproducible checklist, screenshots, scripts                  |         9h | Docs & scripts                        | —                                                                |

**PAD (Exam) — `PAD-F3-B1`**
**Date:** 2026-09-01 · **Deliverable:** complete log (PEB/TEB, modules, regions), scripts, and reproducibility checklist.

---

### `F3-B2` Userland Exploitation I: stack overflow and **basic ROP** (2 weeks · \~60 h)

**Goal:** build and document an **educational exploit** with control-flow diversion and **basic ROP** against lab binaries; clear ethical boundaries.

| Stack                       | Topic Cluster (examples)                                    | Est. Hours | Key Tools             | Assignment (PBR) · Due                                            |
| --------------------------- | ----------------------------------------------------------- | ---------: | --------------------- | ----------------------------------------------------------------- |
| **Classic vulnerabilities** | patterns, offsets, IP/SEH control (instructional scenarios) |        18h | pattern tools, x64dbg | **PBR-F3-B2-1**: IP control + layout · **Due:** 2026-09-06        |
| **Basic ROP**               | gadget hunting in own binaries, minimal chains              |        18h | ROPgadget/`rizin`     | **PBR-F3-B2-2**: Minimal runnable ROP chain · **Due:** 2026-09-13 |
| **Mitigations**             | DEP/ASLR/CFG: impact and limits in lab                      |        12h | WinDbg, docs          | —                                                                 |
| **Evidence & ethics**       | short video, screenshots, scope and rollback                |        12h | Docs                  | —                                                                 |

**PAD (Exam) — `PAD-F3-B2`**
**Window:** 2026-09-12 → 2026-09-14 · **Deliverable:** write-up with steps, tests, known failures, and mitigations.

---

### **EX (parallel) — Bug Bounty Prep (1 week)**

**Check-in:** **Playbook** and checklist ready · **Due:** 2026-09-13.

> Output: operational guide (scopes, evidence, boundaries) to use starting **2026-09-21**.

---

## Q7 — Detailed Schedule

### `F3-B3` Advanced Windows Internals (MM/OBJ/ETW/APC) (4 weeks · \~120 h)

**Goal:** deepen coverage of Memory Manager, Object Manager/handle tables, threads and **APC**, and instrument basic signals with **ETW**.

| Stack              | Topic Cluster (examples)                            | Est. Hours | Key Tools              | Assignment (PBR) · Due                              |
| ------------------ | --------------------------------------------------- | ---------: | ---------------------- | --------------------------------------------------- |
| **Memory Manager** | VADs, working sets, permissions, reserve/commit     |        24h | WinDbg, VMMap          | **PBR-F3-B3-1**: VAD + WS map · **Due:** 2027-08-15 |
| **Object Manager** | object types, duplication/inheritance, handle leaks |        24h | WinDbg, Process Hacker | **PBR-F3-B3-2**: Handle audit · **Due:** 2027-08-22 |
| **Threads & APCs** | queues, early-bird, synchronization                 |        24h | WinDbg                 | **PBR-F3-B3-3**: APC lab PoC · **Due:** 2027-08-29  |
| **Minimal ETW**    | providers, sessions, capturing basic events         |        24h | `wpr`/`xperf`          | —                                                   |
| **Docs & harness** | diagrams, logs, reproducibility                     |        24h | Docs, Python           | —                                                   |

**PAD (Exam) — `PAD-F3-B3`**
**Date:** 2027-09-05 · **Deliverable:** report with memory diagrams and ETW experiments.

---

## Q8 — Detailed Schedule

### `F3-B4` Userland Exploitation II (info leak + ROP/JOP) (5 weeks · \~150 h)

**Goal:** extend exploitation techniques with **info leaks** and applied **ROP/JOP** chains in Windows/Linux lab targets.

| Stack               | Topic Cluster (examples)                               | Est. Hours | Key Tools        | Assignment (PBR) · Due                                                |
| ------------------- | ------------------------------------------------------ | ---------: | ---------------- | --------------------------------------------------------------------- |
| **Info leak**       | instructional strategies to disclose addresses/offsets |        30h | WinDbg, scripts  | **PBR-F3-B4-1**: Reproducible leak + validation · **Due:** 2027-12-12 |
| **Applied ROP/JOP** | building robust chains                                 |        36h | ROPgadget, rizin | **PBR-F3-B4-2**: Stable ROP/JOP chain · **Due:** 2027-12-19           |
| **Lab bypasses**    | permission tweaks, common pitfalls                     |        30h | WinDbg           | **PBR-F3-B4-3**: Documented bypass · **Due:** 2027-12-26              |
| **Validation**      | test harness, stability                                |        24h | Python/C harness | —                                                                     |
| **Docs**            | checklist and write-up                                 |        30h | Docs             | —                                                                     |

**Bridge:** B4→B5 environment sanity · **2028-01-03**
**PAD (Exam) — `PAD-F3-B4`** · **Date:** 2028-01-07.

---

### `F3-B5` Heap Exploitation (LFH vs glibc) (6 weeks · \~180 h)

**Goal:** understand **Windows LFH** vs **glibc** heap models and practice **use-after-free**, **fastbin/tcache**, and **vtable/function-pointer overwrite** in instructional builds.

| Stack            | Topic Cluster (examples)                                | Est. Hours | Key Tools       | Assignment (PBR) · Due                                          |
| ---------------- | ------------------------------------------------------- | ---------: | --------------- | --------------------------------------------------------------- |
| **Heap models**  | LFH vs glibc: allocators, bins, tcache                  |        36h | Debuggers, docs | **PBR-F3-B5-1**: Bin map (lab) · **Due:** 2028-01-14            |
| **Primitives**   | UAF, double free, consolidation, fastbin/tcache         |        48h | PoC labs        | **PBR-F3-B5-2**: Stable UAF with harness · **Due:** 2028-01-28  |
| **Overwrites**   | vtable/function-pointer overwrite, GOT/PLT in parallels |        48h | Ghidra, gdb     | **PBR-F3-B5-3**: Overwrite + control-flow · **Due:** 2028-02-11 |
| **Mitigations**  | basic hardening and validation                          |        24h | Tooling         | —                                                               |
| **Docs & repro** | report, scripts, checklists                             |        24h | Docs            | —                                                               |

**PAD (Exam) — `PAD-F3-B5`**
**Date:** 2028-03-24 · **Deliverable:** stable PoCs, heap diagram, and mitigation paths.

---

## Q9 — Detailed Schedule (closure)

### `F3-B6` Kernel and Driver Fundamentals (Windows) + local elevation (5 weeks · \~150 h)

**Goal:** bring up **KD** and grasp driver models (high-level WDM/WDF), IOCTL/IRP, and produce an instructional **local elevation** using a **vulnerable lab driver**.

| Stack                 | Topic Cluster (examples)                                  | Est. Hours | Key Tools     | Assignment (PBR) · Due                                                  |
| --------------------- | --------------------------------------------------------- | ---------: | ------------- | ----------------------------------------------------------------------- |
| **KD environment**    | WinDbg kernel, symbols, connection                        |        30h | WinDbg KD     | **PBR-F3-B6-1**: KD online + symbols · **Due:** 2028-04-14              |
| **Driver model**      | high-level WDM/WDF, devices, IRP/IOCTL                    |        36h | Docs, samples | **PBR-F3-B6-2**: Benign driver with minimal IOCTL · **Due:** 2028-04-28 |
| **Vulnerable driver** | BYOVD/controlled vulnerable driver; read/write primitives |        36h | Lab driver    | **PBR-F3-B6-3**: Educational EoP with rollback · **Due:** 2028-05-12    |
| **Telemetry**         | minimal ETW/Sysmon for evidence                           |        24h | ETW/Sysmon    | —                                                                       |
| **Docs & OPSEC**      | scope, rollback, checklist                                |        24h | Docs          | —                                                                       |

**PAD (Exam) — `PAD-F3-B6`**
**Date:** 2028-06-02 · **Deliverable:** KD environment design, IRP diagram, and lab elevation evidence.

---

### `F3-CAP` Userland → SYSTEM chain (4–6 weeks · \~120–180 h)

**Goal:** integrate outcomes from B1–B6 into a reproducible, defensible chain (userland → SYSTEM) with telemetry and rollback.

**Milestones & deliverables**

* **Checkpoint 1:** minimal integration with harness · **Due:** 2028-06-16
* **Defense:** technical defense (12–15 min) + demo · **Date:** 2028-07-26
* **Final sign-off (F3):** **2028-07-31** — complete, reproducible evidence; OPSEC/Legal applied.

---

## Express Module (parallel) — **Bug Bounty Playbook**

**Check-ins:** at the close of `F3-B2`, `F3-B4`, and prior to **F3-CAP**
**Deliverable:** operational checklist, report templates, utility scripts. Clearly state ethical boundaries and policies.

---

## Grading & Milestones (Phase 3)

* **PBRs:** weekly, most due on Sundays (see tables).
* **PADs (Exams):** at the end of each block (dates/windows above).
* **Phase 3 Final Sign-off:** **2028-07-31** — all PBR/PAD complete, evidence reproducible, OPSEC/Legal applied, one-command lab repro.
* **Rubric:** A/B/C/Redo per block (stable, well-documented exploit; functional harness; minimal telemetry; clear ethical limits).

---

### Notes

* Dates are planned anchors; the **TOCD pause** between 2026-09-14 and 2027-08-02 does not alter F3 deliverables.
* All work is **benign** and in an **isolated lab**, with snapshots and evidence.
* Codes follow F3 nomenclature (`F3-B1…F3-B6`, `F3-CAP`); PAD = **block-integrated mission**.
