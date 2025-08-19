
# Phase 5 — YoneEvilHost (Kernel · Firmware · UEFI/Boot)

**Syllabus & Schedule (Quarters · Blocks · Stacks)**

**Coverage:** 2029-02-01 → \~2029-07-31
**Cadence:** \~30 h/week (5 h/day, Mon–Sat)
**Methodology:** **PBR** (reproducible labs) + **PAD** (*Practical Aptitude Drill*: block-integrated mission) · Lab-only (OPSEC/Legal)
**Global Outcomes (F5):** F5 environment ready (**KD**, **kprobes/ftrace**, **QEMU+OVMF**, **rollback** policies); **LKM (Linux)** with instructional telemetry and toggles; benign **Windows driver** with minimal **IOCTL** and process/image callbacks; **rootkit-style PoCs** in VM, reversible and detectable via the blue panel; **UEFI/OVMF**: **DXE** inventory and **bootflow** understanding; reproducible documentation/evidence.

---

## Quarter Map (high level)

* **Q12 (2029-02-01 → 2029-05-31):** Pre-flight Bridge · `F5-B1` Kernel Observability & Toolchain · `F5-B2` Linux LKM & Telemetry · `F5-B3` Windows Driver Fundamentals
* **Q13 (2029-06-01 → 2029-07-31):** `F5-B4` UEFI/OVMF & Bootflow · `F5-B5` Rootkit-style PoCs (VM) · **F5-CAP** Capstone

> **Express Module (parallel):** **F5-Express — Rollback & Telemetry Harness** (snapshot scripts, signal diffs, minimal CI). Check-ins at the end of each block.

---

## Q12 — Detailed Schedule

### Pre-flight Bridge (1–2 weeks · \~30–60 h)

**Goal:** align environments (KD/kprobes/QEMU-OVMF), establish a blue baseline, and set rollback policies before moving into kernel/firmware.

| Stack                 | Topic Cluster (examples)                                           | Est. Hours | Key Tools                          | Assignment (PBR) · Due                                                |
| --------------------- | ------------------------------------------------------------------ | ---------: | ---------------------------------- | --------------------------------------------------------------------- |
| **Freeze & Baseline** | freeze F4 (tags, snapshots) · compatibility matrix · Blue baseline |      12–24 | Git, VM mgr, Sysmon/ETW, Sigma/KQL | **PBR-PF-1**: exportable baseline · **Due:** 2029-02-04               |
| **KD + kprobes**      | WinDbg kernel setup · kprobes/ftrace smoke tests · latency checks  |      12–24 | WinDbg KD, ftrace/kprobes          | **PBR-PF-2**: KD/kprobes checklist · **Due:** 2029-02-11              |
| **QEMU+OVMF**         | OVMF vars, Secure Boot (lab), VM templates and snapshots           |        6–8 | QEMU, OVMF/EDK II                  | **PAD-PF**: environment risk/mitigation report · **Date:** 2029-02-12 |

---

### `F5-B1` Kernel Observability & Toolchain (3 weeks · \~90 h)

**Goal:** master basic kernel observability (Windows/Linux) and map signals into the blue panel.

| Stack                | Topic Cluster (examples)                                  | Est. Hours | Key Tools          | Assignment (PBR) · Due                                          |
| -------------------- | --------------------------------------------------------- | ---------: | ------------------ | --------------------------------------------------------------- |
| **Windows KD**       | break-in, symbols, memory, !process/!thread, crash triage |        18h | WinDbg KD          | **PBR-B1-1**: KD playbook · **Due:** 2029-02-18                 |
| **Linux tracing**    | kprobes/kretprobes, ftrace, tracefs, `perf` (overview)    |        18h | ftrace, perf       | **PBR-B1-2**: reproducible tracing recipe · **Due:** 2029-02-25 |
| **QEMU + snapshots** | VM templates, snapshot/rollback scripts                   |        18h | QEMU, Python/bash  | —                                                               |
| **Blue mapping**     | minimal signals (ETW/Sysmon/auditd) vs kernel events      |        18h | Sysmon/ETW, auditd | **PBR-B1-3**: signal↔event table · **Due:** 2029-03-04          |
| **Evidence & risks** | record-keeping discipline and instructional boundaries    |        18h | Docs               | **PAD-B1**: observability report · **Date:** 2029-03-05         |

---

### `F5-B2` Linux LKM & Telemetry (4 weeks · \~120 h)

**Goal:** build benign **LKMs** with telemetry/toggles and validate them against the blue panel.

| Stack                   | Topic Cluster (examples)                          | Est. Hours | Key Tools         | Assignment (PBR) · Due                                                    |
| ----------------------- | ------------------------------------------------- | ---------: | ----------------- | ------------------------------------------------------------------------- |
| **Toolchain & headers** | toolchain, headers/kernel config, DKMS (overview) |        24h | gcc/clang, kbuild | **PBR-B2-1**: LKM skeleton (load/unload/log) · **Due:** 2029-03-11        |
| **Telemetry & sysfs**   | toggles and metrics via `sysfs`/`procfs`          |        24h | kbuild, sysfs     | **PBR-B2-2**: LKM with toggles + tests · **Due:** 2029-03-18              |
| **kprobes/tracepoints** | probes on selected functions; ring buffers        |        36h | kprobes, tracefs  | **PBR-B2-3**: LKM with kprobes + export to userland · **Due:** 2029-03-25 |
| **Stability & safety**  | cleanup, limits, load/rollback testing            |        36h | harness/tests     | **PBR-B2-4**: stress + rollback checklist · **Due:** 2029-04-01           |
| **PAD**                 | practical LKM exam                                |          — | —                 | **PAD-B2**: write-up + evidence · **Date:** 2029-04-02                    |

---

### `F5-B3` Windows Driver Fundamentals (4 weeks · \~120 h)

**Goal:** develop a **benign driver** (high-level KMDF/WDM) with minimal IOCTL and process/image callbacks; lab-signed and reversible.

| Stack                   | Topic Cluster (examples)                                             | Est. Hours | Key Tools        | Assignment (PBR) · Due                                           |
| ----------------------- | -------------------------------------------------------------------- | ---------: | ---------------- | ---------------------------------------------------------------- |
| **KMDF basics**         | project, INF, test signing, load in VM                               |        24h | WDK/VS, signtool | **PBR-B3-1**: driver skeleton + INF · **Due:** 2029-04-08        |
| **Minimal IOCTL**       | queues, dispatch, safe buffers                                       |        24h | KMDF, DevCon     | **PBR-B3-2**: echo IOCTL + logs · **Due:** 2029-04-15            |
| **Notify callbacks**    | process/image (`PsSetCreate*Notify*`, `PsSetLoadImageNotifyRoutine`) |        36h | WDK/WinDbg       | **PBR-B3-3**: callbacks with benign filter · **Due:** 2029-04-22 |
| **Testing & rollbacks** | stability, BSOD triage, rollback checklist                           |        36h | WinDbg, harness  | **PBR-B3-4**: tests + report · **Due:** 2029-04-29               |
| **PAD**                 | short design defense                                                 |          — | —                | **PAD-B3**: demo + QA · **Date:** 2029-05-01                     |

---

## Q13 — Detailed Schedule

### `F5-B4` UEFI/OVMF & Bootflow (3 weeks · \~90 h)

**Goal:** understand **SEC→PEI→DXE** and produce a **benign DXE** that inventories and logs in OVMF with guaranteed rollback.

| Stack                | Topic Cluster (examples)                                | Est. Hours | Key Tools        | Assignment (PBR) · Due                                               |
| -------------------- | ------------------------------------------------------- | ---------: | ---------------- | -------------------------------------------------------------------- |
| **EDK II toolchain** | EDK II tree, `edksetup.sh`, drivers, packaging          |        24h | EDK II, build    | **PBR-B4-1**: EDK II environment + clean build · **Due:** 2029-05-06 |
| **Bootflow & DXE**   | SEC/PEI/DXE, protocols, HII (overview), NVRAM variables |        30h | OVMF, UEFI Shell | **PBR-B4-2**: DXE inventory + variables · **Due:** 2029-05-13        |
| **Benign DXE**       | DXE logging driver + rollback; Secure Boot notes in lab |        36h | EDK II, OVMF     | **PBR-B4-3**: DXE running in VM + evidence · **Due:** 2029-05-20     |
| **PAD**              | block closeout                                          |          — | —                | **PAD-B4**: technical report · **Date:** 2029-05-22                  |

---

### `F5-B5` Rootkit-style PoCs (VM-only) (3 weeks · \~90 h)

**Goal:** **reversible and detectable** PoCs in VM (not production): callback instrumentation/minimal hardening; signal comparison on the blue panel.

| Stack                    | Topic Cluster (examples)                               | Est. Hours | Key Tools          | Assignment (PBR) · Due                                      |
| ------------------------ | ------------------------------------------------------ | ---------: | ------------------ | ----------------------------------------------------------- |
| **Notify & filters**     | filter policies on process/image callbacks             |        30h | WDK/WinDbg, Sysmon | **PBR-B5-1**: PoC with rollback · **Due:** 2029-06-10       |
| **Instructional hiding** | low-surface techniques (lab) and blue-panel validation |        30h | Blue tools         | **PBR-B5-2**: before/after comparison · **Due:** 2029-06-17 |
| **Hygiene & detection**  | rules/queries (YARA/Sigma/KQL) over own artifacts      |        30h | Sigma/KQL, Docs    | **PBR-B5-3**: rules + evidence · **Due:** 2029-06-24        |
| **PAD**                  | technical defense                                      |          — | —                  | **PAD-B5**: report + demo · **Date:** 2029-06-26            |

---

### **F5-CAP** Capstone — Kernel/Firmware Blue-Aware (2–3 weeks · \~60–90 h)

**Goal:** integrate **LKM + Driver + DXE** into a reproducible chain with a blue panel, toggles, and **rollback**; technical defense.

**Milestones & deliverables**

* **Repo `capstone-f5/`** with code, scripts, and a reproducible **README**.
* **Evidence:** logs, screenshots, hashsets; tuned rules/queries.
* **Comparison:** before/after signal (48–72 h).
* **Defense:** brief/slides + demonstration.

**Dates**
**Checkpoints:** 2029-07-08 · 2029-07-22
**Defense:** **2029-07-26**
**Final sign-off (F5):** **2029-07-31**

---

## F5-Express (parallel) — **Rollback & Telemetry Harness**

**Check-ins:** at the close of `F5-B1`…`F5-B5`
**Deliverable:** snapshot/restore scripts, telemetry diffs, test harness with timings/logs. **Sign-off:** **2029-07-31**.

---

## Grading & Milestones (Phase 5)

* **PBRs:** weekly, mostly on Sundays (see tables).
* **PADs (Exams):** at the end of each block (dates/windows above).
* **Phase 5 Final Sign-off:** **2029-07-31** — PBR/PAD complete, evidence reproducible, OPSEC/Legal applied, one-command lab repro.
* **Rubric:** A/B/C/Redo (KD/kprobes/OVMF ready; LKM with toggles and logging; stable lab-signed driver; benign DXE in OVMF; reversible PoCs measured by the blue panel; Capstone with comparative signals).

---

### Notes

* Dates are anchors; minor adjustments do not alter deliverables.
* All work is **benign** and in an **isolated lab**, with snapshots/rollback and evidence.
* Codes follow F5 (`F5-B1…F5-B5`, `F5-CAP`); PAD = **block-integrated mission**.
