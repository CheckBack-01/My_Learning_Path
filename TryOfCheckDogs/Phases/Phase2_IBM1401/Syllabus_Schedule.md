
# Phase 2 — IBM 1401 (Applied Reversing & Userland Execution)

**Syllabus & Schedule (Quarters · Blocks · Stacks)**

**Coverage:** 2026-04-01 → \~2026-07-31
**Cadence:** \~30 h/week (5 h/day, Mon–Sat)
**Methodology:** **PBR** (reproducible labs) + **PAD** (*Practical Aptitude Drill*: block-integrated mission) · Lab-only (OPSEC/Legal)
**Global Outcomes (F2):** reversing report with reproducible **unpack**, **PE parser** and analysis tools, **userland loader** with ≥2 execution techniques, **intro process hollowing** (lab), and discipline of documentation/evidence ready for 8A/8B.

---

## Quarter Map (high level)

* **Q3 (2026-04-01 → 2026-07-31):** `0B04` Applied Reversing I, `1B04` Deep PE & In‑Memory Loaders, `2B04` Userland Paths & Mitigations

> **Express Module (parallel):** **F2-Express — Automation & Tools Harness** — distributed check-ins at each block end; light `tools/` deliverables.

---

## Q3 — Detailed Schedule

### `0B04` Applied Reversing I (6 weeks · \~180 h total)

**Goal:** Master a static/dynamic reversing pipeline (Ghidra/IDA/rizin + x64dbg/WinDbg), identify trivial anti‑analysis, and perform a **single-layer unpack** (e.g. UPX) with minimal IAT reconstruction.

**Stacks & Topics (with hours and assignments)**

| Stack                      | Topic Cluster (examples)                                                       | Est. Hours | Key Tools                         | Assignment (PBR) · Due                                                                                         |
| -------------------------- | ------------------------------------------------------------------------------ | ---------: | --------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Tooling & Baseline**     | Ghidra/IDA/rizin/Cutter, x64dbg/WinDbg setup; memory map; dumps                |       24 h | Ghidra, rizin, x64dbg/WinDbg      | –                                                                                                              |
| **Static Analysis**        | strings/signatures, CFG, calling conventions, struct recovery, common patterns |       30 h | Ghidra/IDA                        | **PBR-0B04-1**: Reversing report (small binary, obfuscated strings) · **Due:** Sun **2026-04-19**              |
| **Dynamic Analysis**       | breakpoints/trace, dump & patch, reloc basics; debugger traps                  |       30 h | x64dbg/WinDbg                     | –                                                                                                              |
| **Anti‑analysis (basics)** | `IsDebuggerPresent`, PEB `BeingDebugged`, time checks; basic bypasses          |       24 h | debugger APIs                     | –                                                                                                              |
| **Packers 101**            | UPX & variants; find OEP; **IAT reconstruction** (tools/scripts propios)       |       24 h | upx, Scylla/ImpRec (lab), scripts | **PBR-0B04-2**: Manual **unpack** + IAT rebuild; hash compare + load in debugger · **Due:** Sun **2026-04-26** |
| **Scripting Support**      | Python helpers (parsers/decoders); automation of dumps                         |       18 h | Python                            | **PBR-0B04-3**: String/config decoder (XOR/RC4 simple) + tests · **Due:** Sun **2026-05-03**                   |

**PAD (Exam) — `PAD-0B04`**
**Window:** **2026-05-18 → 2026-05-20** · **Deliverable:** step‑by‑step methodology, screenshots, checksums before/after, issues & mitigations.

---

### `1B04` Deep PE & In‑Memory Loaders (5 weeks · \~150 h total)

**Goal:** Understand **PE** in practice (headers/sections/imports/exports/relocs/TLS) and build **loaders** that execute benign payloads in memory, up to **intro manual mapping** for a controlled DLL.

| Stack                       | Topic Cluster                                                                      | Est. Hours | Key Tools                | Assignment (PBR) · Due                                                                                            |
| --------------------------- | ---------------------------------------------------------------------------------- | ---------: | ------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| **PE Internals**            | DOS/NT headers, sections vs segments, imports/exports, TLS                         |       30 h | PE-bear, custom parser   | **PBR-1B04-1**: **PE parser** (headers, sections, imports) w/ basic integrity check · **Due:** Sun **2026-05-31** |
| **Proc/Threads/Memory**     | `VirtualAlloc{Ex}`, `WriteProcessMemory`, `Create{Remote}Thread`, `VirtualProtect` |       24 h | Win32 API                | –                                                                                                                 |
| **Loader (local)**          | allocate/copy, perms, controlled jump, error handling                              |       24 h | C/C++                    | **PBR-1B04-2**: **Shellcode loader** (local process) + cleanup/logs · **Due:** Sun **2026-06-07**                 |
| **Manual Mapping (intro)**  | map minimal DLL, imports selectivos, relocs esenciales                             |       24 h | C/C++, PE-bear           | **PBR-1B04-3**: **Manual map** de DLL mínima; ejecutar export · **Due:** Sun **2026-06-14**                       |
| **Inspection & Validation** | PE‑sieve/Process Hacker; stability & crash forensics (lab)                         |       24 h | PE‑sieve, Process Hacker | –                                                                                                                 |
| **Safety & Errors**         | permissions, offsets, alignment; silent crashes                                    |       24 h | logs/asserts             | –                                                                                                                 |

**PAD (Exam) — `PAD-1B04`**
**Date:** **2026-06-22** · **Deliverable:** loader design, memory diagrams, risks, and tests with disciplined error sanitization.

**Q3 Midterm Checkpoint (non‑graded):** **2026-06-03** — short oral defense (10–12 min) on 0B04/1B04 takeaways + mini‑audit of evidence discipline.

---

### `2B04` Userland Paths & Mitigations (5 weeks · \~150 h total)

**Goal:** Implement 2–3 classic **userland execution** techniques and understand impacts of **DEP/ASLR/CFG**, handle policies, and light obfuscation. Prepare for 8A/8B.

| Stack                         | Topic Cluster                                                 | Est. Hours | Key Tools             | Assignment (PBR) · Due                                                                             |
| ----------------------------- | ------------------------------------------------------------- | ---------: | --------------------- | -------------------------------------------------------------------------------------------------- |
| **CRT + LoadLibrary**         | classic inject: `CreateRemoteThread + LoadLibrary`            |       24 h | Win32 API             | **PBR-2B04-1**: Loader with selectable modes (CRT+LL, APC) + logging · **Due:** Sun **2026-07-05** |
| **APC Queueing**              | APC incl. early‑bird; sync considerations                     |       18 h | Win32 API             | –                                                                                                  |
| **Process Hollowing (intro)** | hollowing vs module stomping; reversible lab demo             |       24 h | Windows tooling       | **PBR-2B04-2**: **Hollowing PoC** vs lab binary + rollback evidence · **Due:** Sun **2026-07-12**  |
| **PPID & CreateProcess**      | PPID spoofing, useful flags for staging                       |       12 h | Win32 API             | –                                                                                                  |
| **Light Obfuscation**         | API hashing, string hiding; minimal config sealing            |       18 h | C/C++                 | –                                                                                                  |
| **Mitigations & Telemetry**   | DEP/ASLR/CFG; lab AV/signing; artifact surfaces; quick traces |       24 h | Sysmon/ETW (lab), KQL | **PBR-2B04-3**: **Trace comparison** across techniques + checklist · **Due:** Sun **2026-07-19**   |

**PAD (Exam) — `PAD-2B04`**
**Date:** **2026-07-28** · **Deliverable:** mitigations analysis, detection surfaces, and improvement plan for F3 + 8A/8B.

---

## Express Module (parallel) — **F2-Express: Automation & Tools Harness**

**Check-ins:** end of each block (`0B04`, `1B04`, `2B04`)
**Deliverable:** versioned `tools/` with Python/C scripts (parsers, string/config extractors), loader test harness (I/O, logs, timers), and seed datasets. **Final sign‑off:** **2026-07-31**.

---

## Grading & Milestones (Phase 2)

* **PBRs:** weekly, due most Sundays (see tables).
* **PADs (Exams):** at block ends (dates above).
* **Phase 2 Final Sign-off:** **2026-07-31** — all PBR/PAD complete, evidence reproducible, OPSEC/Legal discipline applied, one‑command lab repro OK.
* **Rubric:** A/B/C/Redo per F2 spec (unpack clean, parser usable, ≥2 loader modes, hollowing PoC stable, reproducible docs).

---

### Notes

* Dates are planned anchors; minor shifts won’t alter deliverables.
* All work is **lab‑only**, with **benign** payloads, snapshots, and **reproducible** evidence.
* Block codes follow F2 nomenclature (`0B04`…`2B04`); PAD = **block‑integrated mission**.
