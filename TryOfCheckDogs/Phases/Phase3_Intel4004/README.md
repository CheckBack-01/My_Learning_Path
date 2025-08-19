
# Phase 3 — Intel 4004 (Userland Internals & Exploitation)

**Scope.** Phase 3 covers **userland internals** (processes/memory) and **introductory, hands-on exploitation** in userland, scaling from basic ROP to information leaks and kernel R/W primitives in a **lab** environment.

**Methodology.** Each block concludes with **PBR** (reproducible lab) + **PAD** (Practical Aptitude Drill: a block-level integrated mission with evidence and replication steps). OPSEC/Legal is applied throughout.

**Phase-level outcomes.**
• Internals log (PEB/TEB, modules, heaps, regions) plus inventory utilities • **Educational exploit** using **basic ROP** with mitigation analysis • **Userland exploits** on Win/Linux with info-leak + ROP/JOP (instructional) • **Heap** PoCs (LFH/tcache) • **R/W primitive** via a lab vulnerable driver and controlled **local elevation** • **Capstone**: userland → SYSTEM chain with documentation and reproducible evidence.

---

## How Phase 3 is organized

**Nomenclature.** Blocks use codes like `0B04`, where `X` is the zero-based block index and `YY` is the number of stacks within that block (if applicable).

**Blocks in Intel 4004**

### `0B04` — Process & Memory Internals (userland, Windows/ELF in parallel)

**Goal.** Understand process/thread anatomy: **PEB/TEB**, memory layout, modules, heaps, and regions; practice inspection with debuggers and utilities.
**Highlights.** PEB/TEB, process parameters, Ldr module list; regions (image/heap/stack/private), reserve vs commit and permissions; module load/order and basic resolution (with PLT/GOT parallels in ELF); high-level view of SEH/VEH; inspection methodology (breakpoints, structure queries, module/region maps) and evidence logging.
**PBR examples.** (1) **Process map** with a custom script (modules, regions, permissions → JSON/CSV). (2) **PEB/TEB walk** extracting key fields (image path, argv, modules). (3) **TLS callback demo**: identify order and demonstrate load-time execution for a lab DLL.
**PAD evidence.** Report with layout diagrams, debugger screenshots, and PE vs ELF comparison; versioned scripts and reproducible steps.

### `1B03` — Userland Exploitation I: stack overflow & basic ROP (lab)

**Goal.** Build and document an **educational exploit** against a lab-vulnerable binary using **basic ROP** to bypass **DEP/ASLR** in a didactic setting.
**Highlights.** High-level review of mitigations (DEP/ASLR/CFG); classic stack overflow conditions in lab binaries; **basic ROP** (gadgets from the target, simple chains for register/permission adjustments and control transfer); pedagogical strategies: invoke already-present functions with safe arguments or change permissions on a benign region prior to a controlled jump; minimal exploit telemetry.
**PBR examples.** (1) **Educational exploit** with elementary ROP that yields a safe, observable effect. (2) **Mitigation analysis**: how defenses influenced the chain and scenario assumptions. (3) **Post-mortem hardening**: compilation flags that neutralize the lab exploit.
**PAD evidence.** Technical report with threat model, assumptions, steps, screenshots/traces, and limitations; legal/ethics checklist for the scenario.

### `EX0B01` — Express F3: Bug bounty preparation (pre-window)

**Goal.** Finalize playbook, evidence, and schedule for the **bug bounty** window.
**Highlights.** Report and severity templates; daily recon/triage (authorized programs); evidence pipeline (capture, redaction of sensitive data, versioning); schedule and personal metrics.
**Deliverable.** Report template; structured `evidence/` folder; list of in-policy programs; weekly schedule and metrics.

### `2B04` — Advanced Windows Internals (MM, Object Manager, ETW, threads/APC)

**Goal.** Understand critical Windows subsystems (Memory Manager, Object Manager, scheduler/threads), and capture minimal signals with **ETW**.
**Highlights.** **MM**: VADs, protections, reserve/commit, high-level working sets; **Object Manager/Handle Tables**: types, duplication, inheritance, leaks; **Threads/APCs**: queues, early-bird, synchronization; **ETW** intro: providers for processes/images/threads/loaders; tooling: WinDbg with symbols, Process Hacker, VMMap, ETW.
**PBR examples.** (1) **Handle map** filtered by type/process → CSV. (2) **Region map** with permissions and code/data heuristics. (3) **APC demo** executing a benign function with logs. (4) **ETW capture** for process/image creation/loading with brief analysis.
**PAD evidence.** Report with diagrams and artifacts; limits and risks.

### `3B03` — Userland Exploitation II: info-leak + ROP/JOP (Win/Linux)

**Goal.** Build userland exploits with **information leaks** to defeat ASLR and chain **ROP/JOP** to address DEP/CFG in lab scenarios.
**Highlights.** **Info-leaks**: out-of-bounds reads, printed pointers, basic side channels; **ROP/JOP** with gadget selection and alignment pitfalls; mitigations (DEP/ASLR/CFG/RELRO on Linux) and impact; hygiene: reliability, cleanup, and minimal telemetry.
**PBR examples.** (1) **Windows exploit** with leak + ROP that invokes an observable API without crashing. (2) **Linux exploit** with a leak and a chain that calls `mprotect` or equivalent. (3) **Automated test harness** per exploit (success/failure, timings, logs).
**PAD evidence.** Write-ups with chain diagrams, gadgets, offsets, and encountered mitigations.

### `4B03` — Heap exploitation (Windows LFH vs Linux glibc) — lab

**Goal.** Understand modern heap models and practice **UAF**, **tcache/fastbin poisoning** (Linux), and **vtable/func-ptr overwrite** (Windows) in instructional builds.
**Highlights.** **Windows**: LFH, simple grooming, UAF patterns, vtable/func-ptr overwrite; **Linux (glibc)**: educational fastbins/tcache, consolidation, controlled bin collisions; **Defenses**: build hardening, validation with ASan/UBSan.
**PBR examples.** (1) **UAF PoC (Win)** that controls a function pointer. (2) **tcache/fastbin PoC (Linux)** with overwrite to an observable effect. (3) **Mitigations**: recompile with security options and demonstrate PoC neutralization.
**PAD evidence.** Documentation with primitives, heap diagram, and grooming steps.

### `5B05` — Kernel (Windows) fundamentals + local elevation (lab)

**Goal.** Set up a **kernel debugging** environment and understand the **IOCTL/IRP** flow; obtain an **R/W primitive** via a lab vulnerable driver and perform an educational **local elevation**.
**Highlights.** Driver model (high-level WDM/WDF), devices, IOCTL, IRP; KD environment (WinDbg, symbols); lab-vulnerable drivers (arbitrary read/write, truncation, etc.); **R/W primitive** → token stealing or a benign credential patch in a VM; safety: strict limits and snapshots.
**PBR examples.** (1) **IOCTL client** for the lab driver (enumerate/invoke controls). (2) **Working R/W primitive** with tests. (3) **Elevation to SYSTEM** in a VM with evidence and rollback.
**PAD evidence.** Report with driver architecture, IRP flow, exploit design, and rollback steps.

### `6B02` — F3-CAP: Full chain (userland → SYSTEM) — lab

**Goal.** Integrate skills: userland execution with your own exploit and **local elevation** using an R/W primitive from a vulnerable lab driver. Defend the solution in a technical presentation.
**Highlights.** Prepare the **userland PoC** (from B3/B4) as the first link; integrate **IOCTL client** and the R/W primitive (B5) to escalate to SYSTEM; **Hardening** and countermeasures (mitigated builds and demonstration of neutralization); evidence: timings, harness, checksums, short video.
**Deliverable.** `capstone-f3/` repo with code, scripts, and a reproducible `README.md`; evidence (logs, screenshots, hashsets) and technical defense (slides or document).

---

## What you’ll learn (skills & mindset)

* Userland process and memory internals (PEB/TEB, modules, regions, heaps).
* Userland exploitation from basic ROP to JOP with information leaks in lab scenarios.
* Minimal instrumentation with ETW and artifact analysis.
* Heap practice (LFH/tcache) with a pedagogical focus and mitigations.
* Windows kernel fundamentals (IOCTL/IRP) and **educational** local elevation in a VM.
* End-to-end integration in a reproducible, defensible Capstone.

---

## Outcomes & success criteria

* Utilities/scripts: process inventory, PEB/TEB extraction, TLS demo.
* **Educational exploit** using basic ROP with evidence and mitigation analysis.
* **Win/Linux exploits** with info-leak + ROP/JOP and automated harnesses.
* Stable **heap PoCs** with verified hardening.
* **Kernel R/W primitive** in a lab and **elevation to SYSTEM** with safe rollback.
* **Capstone** with a reproducible full chain and technical defense.
* Phase-level grading: **A** = complete PBR/PAD; stable exploits/PoCs; useful utilities; solid, well-documented Capstone. **B** = ≥80% with items to polish; **C** = ≥60% with partial reproducibility; **Redo** = <60% or deficient ethical scope.

---

## PBR & PAD — how we evaluate

* **PBR (Proof-of-Bounty-Readiness).** Reproducible lab with explicit objectives, verifiable steps, and artifacts (code, logs, screenshots, hashsets).
* **PAD (Practical Aptitude Drill).** Block-level integrated mission; evaluative, with risks/limitations and **reproducible** in your lab.

> Each block closes with **PBR + PAD** and a minimal evidence package.
