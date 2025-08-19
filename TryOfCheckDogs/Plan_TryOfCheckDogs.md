
# PLAN — Try Of Check Dogs (TOCD)

**Author:** Denis Pérez  
**Last updated:** 2025-08-10

---

## 1) Vision & Goal

Achieve professional competence in **Reverse Engineering (RE)** and **Malware Development**. The intended outcome is a portfolio of **verifiable projects**: exploits and post-exploitation, implants with **C2** and **persistence**, **evasion techniques validated via telemetry**, and documentation aligned with professional standards.

---

## 2) Route Principles

- **Hands-on first:** every block includes **PBR** (reproducible labs) and **PAD**  
  (**Practical Aptitude Drill:** a **block-closing**, **integrated**, multi-technique mission with evaluative criteria and reproducible evidence).
- **Objective measurement:** defensive baseline (Sysmon/ETW, YARA/Sigma, KQL) to demonstrate evasion **with data**.
- **Ethics & isolation:** all work occurs in an **isolated lab** under **OPSEC/Legal** controls.
- **Realistic progression:** from fundamentals to kernel/UEFI **without artificial jumps**.

> *Block nomenclature (when referenced elsewhere):* F1–F3 use `XBYY` (e.g., `0B04`) — `X` = block index starting at 0; `YY` = number of stacks. F4 uses `F4-B1…B5` plus modules **8A/8B/9B**. F5 uses `B1…B5`.

---

## 3) Schedule

- **TOCD Segment 1:** **2025-08-14 → 2026-09-14**  
  Intensive self-study (5 h/day, Mon–Sat). PBR/PAD deliverables per block.
- **Break:** **2026-09-14 → 2026-09-20**  
  Six-day pause. Small BackLogs if needed to maintain pace.
- **Bug Bounty + University start:** **2026-09-21 → 2027-07-21**  
  First 9 months of university in parallel with bug hunting (4–5 h/day); TOCD via **BackLogs** (6–8 h/week).
- **TOCD resumes without pauses:** **from 2027-08-03** until all phases are complete.
- **Estimated TOCD completion:** **53 months → 2030-01-18 to 2030-02-03**

> The **JHU** master’s program will begin once employment makes it sustainable, **without interrupting TOCD**.

---

## 4) Coordinated Tracks

1. **TOCD (self-directed):** custom, progressive curriculum focused on systems, RE, exploit dev, and evasion.  
2. **University (TEP PUCMM):** formal cybersecurity foundation. Start: **2026-09**. Estimated duration: ~2 years (through 2028).  
3. **Master’s (JHU):** pursued after securing RE/maldev-related employment.

---

## 5) Phase Structure (summary)

- **Phase 1 — Systems & programming fundamentals**  
  Linux/CLI, C/C++, assembly, architecture. **Goal:** low-level fluency.

- **Phase 2 — Applied analysis & initial RCE**  
  Applied reversing, payloads, client-side surface.

- **Phase 3 — Advanced RE & OS internals**  
  Userland and kernel internals, advanced exploit dev, integrative projects.

- **Phase 4 — Evasion, persistence, and operations**  
  Anti-debug/anti-VM, unhooking, direct syscalls, hollowing, module stomping, **C2**, and covert operations.  
  - **8A (new):** Initial Access & covert delivery (maldocs, LNK/HTA/JS, AMSI, LOLBins, WMI).  
  - **8B (new):** Minimal Blue Track (Sysmon/ETW, YARA/Sigma, KQL) for baseline & validation.  
  - **9B (new):** Implant crypto & Packer v2 (proper AEAD, key rotation, light mutation).

- **Phase 5 — Advanced persistence & firmware**  
  Rootkits/bootkits, UEFI, and a final project with technical defense.  
  - **Extensions 12A–12F (optional):**  
    **12A** macOS Internals + EndpointSecurity · **12B** Linux EDR/eBPF · **12C** Android ARM64 + basic Frida ·  
    **12D** Hardware RE basics (UART/JTAG/SWD, SPI flash) · **12E** Bus sniffers & firmware pipeline · **12F** Glitching/FPGA lite.

- **Express Module (new):** **OPSEC & Legal** for secure builds, compartmentalization, and usage limits.

---

## 6) Time Commitments

- **Before university:** 5 h/day, Mon–Sat, on TOCD.  
- **Bug Bounty + university (9 months):** 4–5 h/day on bugs; TOCD via **BackLogs** (6–8 h/week).  
- **From 2027-08-03:** TOCD continues without pauses until completion (full pace).

---

## 7) Goals & KPIs

**Technical goals**
- Close each block’s **PBR + PAD** with **reproducible evidence** (screenshots, hashset, IOC list, report).  
- Capstone with a full chain: initial access → execution → persistence/rootkit → C2 → Blue validation.

**Progress KPIs**
- Effective lab hours per week.  
- Detection rate vs attempts in **8B** (signal/noise).  
- PBR/PAD closed per block and per phase.  
- Public bug-bounty cases during 2026–2027 (target: **1–2/month**).

**Financial goal**
- Operating target: **USD 10,000–24,000** during the bug-bounty window (2026-09-21 → 2027-07-21) to support living expenses and studies.  
- Cushion: **3–4 months** of expenses; logging and post-mortems for each case.

---

## 8) BackLogs during university

During the 9-month bug bounty + university period, maintain TOCD with **6–8 h/week BackLogs**:
- Quick refreshers of completed labs to avoid decay.  
- Mini-exercises for **8A/8B** (rule tuning, new delivery chains).  
- Toolchain and documentation maintenance.

---

## 9) Risk Management

- **Academic overload:** prioritize critical deliverables; limit TOCD to BackLogs.  
- **Income volatility:** savings plan and steady reporting pipeline for bug bounty.  
- **Scope drift:** no new modules until **8A/8B/9B/12A–12F** are complete.  
- **Ethics/Legal:** lab-only testing and explicit consent in controlled cases.

---

## 10) OPSEC & Legal

- Campaign-level project compartmentalization.  
- Metadata minimization (PDB/RSDS, timestamps, FileVersionInfo).  
- Signing and artifact control where applicable.  
- Usage policies and consent documentation.

---

## 11) Versioning & Control

- Separate repos per phase/block.  
- Issues and Milestones aligned to KPIs.  
- Changelog/lab log with dated entries (ISO-8601 + local time).

---

## 12) High-Level Calendar (summary)

- **2025-08-14 → 2026-09-14:** Continuous TOCD (5 h/day).  
- **2026-09-14 → 2026-09-20:** Break (6 days).  
- **2026-09-21 → 2027-07-21:** Bug Bounty + University (TOCD via BackLogs).  
- **From 2027-08-03:** TOCD without pauses until finish (ETA 2029-12-03 / 2030-01-18 → 2030-02-03).

---

## 13) Expected Outcome

By the end, I will have **operational RE/maldev skills**, a portfolio of **verifiable projects**, **measured evasion** backed by telemetry, 
and **professional-grade documentation**—ready for a specialized role and the JHU master’s program.
```
