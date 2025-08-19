
# Phase 5 — YoneEvilHost (Kernel, Firmware, UEFI/Boot)

**Scope.** Phase 5 consolidates **kernel observability and development** (Linux/Windows) and an **operational understanding of UEFI/bootflow** in a **lab-only** environment (VM + OVMF). All work is **benign**, reproducible, and governed by **OPSEC/Legal**.

**Methodology.** Each block concludes with **PBR** (reproducible lab) + **PAD** (Practical Aptitude Drill: a block-level integrated mission with evidence and replication steps).

**Phase-level outcomes.**
• F5 environment ready (KD, kprobes/ftrace, QEMU+OVMF, rollback policies) • **Linux LKM** with instructional telemetry and toggles • **Benign Windows driver** with minimal IOCTL and process/image callbacks • **Rootkit-style PoCs** in a VM, reversible and detectable with your blue-team panel • **UEFI/OVMF**: DXE inventory and a **benign DXE** that logs at boot • **Bootflow**: educational DXE module with tests under Secure Boot on/off • **F5 Capstone**: kernel + firmware chain with technical defense and proven rollback.

---

## How Phase 5 is organized

**Nomenclature.** Blocks use codes like `0B01`, where `X` is the zero-based block index and `YY` is the number of stacks within that block (if applicable).

**Blocks in YoneEvilHost**

### `0B01` — F5 Pre-flight (readiness for kernel/firmware)

**Goal.** Prepare a **safe environment** for kernel and firmware practice.
**Highlights.** Clean VM (Win/Linux) and OVMF snapshots; WinDbg KD and symbols; `dmesg`, `ftrace`, `kprobes`; QEMU + OVMF/edk2; firmware tools (UEFITool/UEFIExtract, CHIPSEC in analysis mode, `sbctl`/`mokutil`, read-only `fwupd`); tested **rollback** and restore policies.
**PBR examples.** (1) Verify kernel debugging (Win/Linux) with a controlled hello-world. (2) Launch QEMU+OVMF and extract volumes with UEFITool. (3) Risk document and recovery plan.
**PAD evidence.** Readiness report with risks, mitigations, and rollback steps.

### `1B04` — Advanced Linux Kernel: LKMs, kprobes/ftrace, and telemetry

**Goal.** Understand the module lifecycle and practice **noninvasive** instrumentation with kprobes/kretprobes/ftrace; expose metrics via `/proc` or `/sys`.
**Highlights.** Minimal Kbuild/Kconfig, symbols and signing; high-level review of core structs (`task_struct`, `files_struct`); **kprobes/kretprobes** and **ftrace**; metrics export (`seq_file`, `sysfs`); lab safety: avoid destructive hooks.
**PBR examples.** (1) **LKM** exposing process info (PID, cmdline) via `/proc/demo_lkm`. (2) Instrument a selected syscall with kprobes and controlled logging. (3) Performance and stability report using `perf`/traces.
**PAD evidence.** Module design, risks, test results, and build guide.

### `2B05` — Windows Kernel fundamentals: WDM/WDF, IOCTL/IRP, and callbacks

**Goal.** Build a **benign driver** that logs process/image events and exposes a simple IOCTL; debug in KD.
**Highlights.** High-level WDM/WDF model and IRP lifecycle; symbolic devices/queues and lab access control; process/image **callbacks** (`PsSetCreateProcessNotifyRoutineEx`, `PsSetLoadImageNotifyRoutine`); IOCTL with buffer validation; telemetry to debugger and basic traces.
**PBR examples.** (1) Driver that logs process/image creation to the debugger. (2) Userland client consuming an IOCTL and receiving a counter/state. (3) VM deployment/rollback script with tests.
**PAD evidence.** Architecture, IRP flow, IOCTL safety, and test results.

### `3B05` — Rootkit techniques in the lab (safe, multi-OS)

**Goal.** Study **historical and modern** concealment/monitoring patterns in userland/kernel, implementing **benign, reversible PoCs** in a VM.
**Highlights.** **Linux:** instructional interception with kprobes/ftrace; event filtering without altering functional behavior. **Windows:** process/image/registry callbacks; minifilter concept for controlled logging. Modern considerations (PatchGuard, control-flow) and pedagogical limits. Anti-analysis/detection: identify your own PoCs from the blue-team side.
**PBR examples.** (1) Linux PoC selectively logging `open/exec` via kprobes with a sysfs toggle. (2) Windows PoC with non-disruptive registry/log filter and IOCTL toggles. (3) Blue validation: YARA/Sigma rules and KQL queries to detect your PoCs.
**PAD evidence.** Documentation, risks, and a full rollback guide.

### `4B04` — UEFI internals and firmware analysis (OVMF/QEMU)

**Goal.** Understand **UEFI** architecture (PEI/DXE/RT), analyze volumes/modules in **OVMF**, and instrument a **benign DXE** that logs an event.
**Highlights.** UEFI phases, services, and protocols; high-level Secure Boot; tools: UEFITool/UEFIExtract, `chipsec_util` (analysis), edk2 builds; QEMU bootflow with OVMF; lab NVRAM variables; safety: NVRAM backups and guaranteed rollback.
**PBR examples.** (1) Extract and inventory OVMF DXE modules and map dependencies. (2) Build a **benign DXE driver** that logs during boot in QEMU. (3) Secure Boot report: state, keys, and observed execution paths.
**PAD evidence.** Write-up with steps, screenshots, and risks.

### `5B05` — Bootflow and educational bootkit practices in a VM

**Goal.** Explore the **full bootflow** in a virtual environment and build an **educational module** that modifies a **benign** boot parameter (telemetry or banner), demonstrating **mitigations** with Secure Boot.
**Highlights.** Bootflow from firmware to OS handoff; historical hook locations (study); edk2 project structure, build, and lab signing; Secure Boot and the chain of trust; policy on/off effects; blue evaluation: change and integrity detection.
**PBR examples.** (1) **Harmless** DXE boot module that shows a banner/log. (2) Impact measurement with Secure Boot on/off and documented differences. (3) Provisioning and restore script for NVRAM/OVMF.
**PAD evidence.** Risk report, mitigations, and recovery procedure.

### `6B02` — F5-CAP: Kernel/firmware chain with technical defense

**Goal.** Integrate skills in a **VM**: kernel telemetry (Linux or Windows) + **benign** OVMF boot component; blue-team evaluation and technical defense.
**Highlights.** Path A (Linux LKM + benign DXE) or Path B (Windows driver + benign DXE); stability, performance, and detectability tests using your blue panel; documentation, build and rollback scripts; technical defense.
**Deliverable.** `capstone-f5/` repo with code, scripts, reproducible `README`, evidence, and presentation; OPSEC/Legal checklist applied and signed.

---

## What you’ll learn (skills & mindset)

* **Kernel** observability and development (Linux/Windows) with benign artifacts.
* Instructional instrumentation with **kprobes/ftrace** and kernel callbacks (Windows).
* **UEFI/OVMF**: DXE analysis and a benign driver built with edk2.
* Comparative **bootflow** and **Secure Boot** effects with metrics.
* Blue validation: YARA/Sigma rules, KQL, and your own observability panel.
* **Rollback** discipline and reproducible documentation in VMs.

---

## Outcomes & success criteria

* Kernel/firmware environment ready and validated; recovery policies active.
* **LKM** with metrics in `/proc`/`/sys` and controlled kprobes/ftrace.
* **Windows driver** with IOCTL and process/image callbacks, stable under KD.
* **Lab PoCs** that are reversible and **detectable** by your own rules.
* **Benign DXE** in OVMF logging at boot; stable VM; verified rollback.
* **Educational DXE** module with a benign effect and Secure Boot on/off comparison.
* **F5 Capstone** reproducible, no bricking, with metrics and a convincing defense.
* Phase-level grading: **A** = complete PBR/PAD; stable, reversible PoCs; functional benign DXE; strong Capstone with blue validation and impeccable rollback. **B** = ≥80% PBR/PAD; some instability documented; functional Capstone. **C** = ≥60% PBR/PAD; partial reproducibility or weak blue validation. **Redo** = <60% or operational risk (no proven rollback).

---

## PBR & PAD — how we evaluate

* **PBR (Proof-of-Bounty-Readiness).** Reproducible lab with explicit objectives, verifiable steps, and artifacts (code, logs, screenshots, hashsets).
* **PAD (Practical Aptitude Drill).** Block-level integrated mission; evaluative, with risks/limitations and **reproducible** in your lab.

> Each block closes with **PBR + PAD** and a minimal evidence package.
