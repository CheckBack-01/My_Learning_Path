
### **Phase 2 — IBM 1401 (Applied Analysis & RCE)**

#### **Syllabus & Schedule (Quarters · Blocks · Stacks)**

**Coverage:** 2026-03-09 → \~2026-07-26  
**Cadence:** \~30 h/week (5 h/day, Mon–Sat)  
**Methodology:** PBR (reproducible labs) + PAD (Practical Aptitude Drill) · Lab-only (OPSEC/Legal)  
**Global Outcomes (F2):** Reversing report with reproducible unpack, a custom PE parser, a userland loader with at least two execution techniques, and an introductory process hollowing PoC.

-----

#### **Quarter Map (high level)**

  * **Q2 (2026-03-09 → 2026-05-31):** `0B04 Reversing & Unpack`, `1B04 PE Format & Loaders` (start).
  * **Q3 (2026-06-01 → 2026-08-30):** `1B04` (wrap-up), `2B04 Userland Execution Routes`, `3B02 F2→F3 Bridge & Capstone`.
  * **Express Module (parallel):** `EX0B01 — F2 Tooling & Automation` — distributed slots throughout the phase.

-----

### **Q2 — Detailed Schedule**

#### **0B04 — Reversing, Anti-Analysis & Unpack (6 weeks · \~180 h total)**

**Goal:** Master the static/dynamic analysis pipeline, identify trivial anti-analysis, and perform a manual unpack with IAT reconstruction.

| Stack/Topic Cluster (examples) | Est. Hours | Key Tools | Assignment (PBR/PAD) · Due |
| :--- | :--- | :--- | :--- |
| **Static Flow & Triage**\<br\>CFG, strings, signatures, function mapping, struct recovery | 30 h | Ghidra, rizin, PE-bear | **PBR-0.1:** Reversing report template design · Due: Sun 2026-03-22 |
| **Dynamic Flow & Anti-Analysis**\<br\>Breakpoints, memory maps, PEB flags, `IsDebuggerPresent` bypass | 30 h | x64dbg, WinDbg | **PBR-0.2:** Reproducible dynamic analysis session · Due: Sun 2026-04-05 |
| **Packers & OEP**\<br\>UPX variants, OEP finding strategies, dumping from memory | 45 h | x64dbg, Scylla | – |
| **IAT Reconstruction**\<br\>Manual and tool-assisted IAT repair, validation of dumped binary | 45 h | Scylla, PE-bear, x64dbg | **PBR-0.3:** Manual unpack of lab sample (clean dump + functional IAT) · Due: Sun 2026-04-12 |
| **Support Scripting**\<br\>String/config decoders (XOR/RC4), unit tests | 30 h | Python | **PBR-0.4:** Operational decoder script + test suite · Due: Sun 2026-04-19 |
| **PAD (Exam) — PAD-0**\<br\>Integrated mission: full analysis + unpack of new sample. | | | Window: 2026-04-20 → 2026-04-22 · Deliverable: final report, scripts, and checksums. |

-----

#### **1B04 — PE Format, Windows API & Memory Loaders (5 weeks · \~150 h total)**

**Goal:** Understand the PE format practically and build loaders that execute payloads from memory, from simple shellcode to basic manual mapping.

| Stack/Topic Cluster | Est. Hours | Key Tools | Assignment (PBR/PAD) · Due |
| :--- | :--- | :--- | :--- |
| **PE Fundamentals & Parser**\<br\>DOS/NT headers, sections, imports, exports, relocs, TLS | 45 h | C/C++, Python | **PBR-1.1:** PE parser for headers, sections & imports · Due: Sun 2026-05-03 |
| **Local Shellcode Loader**\<br\>`VirtualAlloc`, `VirtualProtect`, payload copy, controlled jump, cleanup | 45 h | C/C++, x64dbg | **PBR-1.2:** Stable local loader with error handling · Due: Sun 2026-05-17 |
| **Manual Mapping Intro**\<br\>Selective import resolution, essential relocations, entrypoint call | 45 h | C/C++, PE-bear | **PBR-1.3:** Manual map of a minimal DLL and export execution · Due: Sun 2026-05-24 |
| **Validation & Inspection**\<br\>Verifying in-memory artifacts and loader stability | 15 h | PE-sieve, Process Hacker | – |
| **PAD (Exam) — PAD-1**\<br\>Consolidated report: loader design, memory diagrams, risks & tests. | | | Date: 2026-05-28 · Deliverable: full code repository and technical write-up. |

-----

### **Q3 — Detailed Schedule**

#### **2B04 — Userland Execution Routes & Mitigations (5 weeks · \~150 h total)**

**Goal:** Implement classic injection techniques and understand the impact of modern mitigations like DEP, ASLR, and CFG.

| Stack/Topic Cluster | Est. Hours | Key Tools | Assignment (PBR/PAD) · Due |
| :--- | :--- | :--- | :--- |
| **Classic Injection (CRT+LL)**\<br\>`CreateRemoteThread` + `LoadLibrary`, handle management, logging | 30 h | C/C++, Process Hacker | **PBR-2.1:** Functional CRT+LL injection mode in loader · Due: Sun 2026-06-07 |
| **APC Queueing**\<br\>APC/early-bird concepts, synchronization, failure points | 45 h | C/C++, WinDbg | **PBR-2.2:** Operational APC injection mode with evidence · Due: Sun 2026-06-14 |
| **Introductory Hollowing**\<br\>Process creation, memory unmapping, section writing, context switching | 45 h | C/C++, x64dbg | **PBR-2.3:** Process Hollowing PoC on a lab binary · Due: Sun 2026-06-21 |
| **Mitigations & Trace Analysis**\<br\>DEP/ASLR/CFG, PPID spoofing, detection surfaces | 30 h | PE-sieve, Sysmon | **PBR-2.4:** Comparative trace analysis of injection techniques · Due: Sun 2026-06-28 |
| **PAD (Exam) — PAD-2**\<br\>Final report: analysis of mitigations and operational trade-offs. | | | Date: 2026-07-01 · Deliverable: comparative report and future improvement plan. |

-----

#### **3B02 — Bridge F2 → F3 & Capstone (2 weeks · \~60 h total)**

**Goal:** Consolidate F2 evidence into an "audit-ready" package and prepare the lab environment for F3's userland internals and exploitation modules.

| Stack/Topic Cluster | Est. Hours | Key Tools | Assignment (PBR) · Due |
| :--- | :--- | :--- | :--- |
| **F2 Evidence Consolidation**\<br\>Clean re-runs, telemetry capture, refactoring, evidence curation | 30 h | Git, PE-sieve, Python | **PBR-3.1 & 3.2:** "Ready-to-hand-off" evidence packages · Due: Sun 2026-07-12 |
| **F3 Environment Warm-up**\<br\>WinDbg setup, PEB/TEB cheatsheets, skeleton tools, ROP harness | 30 h | WinDbg, Python, Git | **PBR-3.3 & 3.4:** "Warm-up F3" kit and auto-bootstrapping environment · Due: Sun 2026-07-19 |
| **PAD (Exam) — PAD-3**\<br\>Bridge report: final F2 status, risks, and F3 entry plan. | | | Date: 2026-07-22 · Deliverable: Final bridge report and F3 roadmap. |

-----

#### **Express Module (parallel) — EX0B01: F2 Tooling & Automation**

  * **Check-ins:** Weekly slots of 1-2 hours distributed throughout Q2 and Q3.
  * **Deliverable:** Versioned `tools/` directory with documented scripts and test harnesses. Final sign-off by **2026-07-24**.

-----

#### **Grading & Milestones**

  * **PBRs:** Due most Sundays (see tables).
  * **PADs (Exams):** At block ends (dates above).
  * **Phase 2 Final Sign-off:** **2026-07-26** — All PBR/PADs complete, evidence reproducible, tools versioned, F3 environment is ready.
  * **Rubric:** A/B/C/Redo per spec (loader stability, parser utility, documentation clarity).

-----

#### **Notes**

  * This schedule is a focused plan. Minor date shifts are acceptable, but deliverables are fixed.
  * All work is strictly confined to lab VMs using benign payloads and with snapshots for recovery.
  * Block codes (`0B04`...`3B02`) align with your detailed project breakdown for precise tracking.
