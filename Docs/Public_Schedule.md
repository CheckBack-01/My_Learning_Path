
# Public Schedule — TOCD (Quarters, Phases, Blocks & Stacks)

> **Coverage:** 2025-08-14 → 2030-02-03
> **Time commitment:** 5 h/day (Mon–Sat)
> **Methodology:** **PBR** (reproducible labs) + **PAD** (*Practical Aptitude Drill*: **block-integrated mission**, multi-technique and evaluative) · OPSEC/Legal enforced
> **Nomenclature:**
> • F1–F3 blocks follow `XBYY` (e.g., `0B04`) → `X` = block index starting at 0 · `YY` = number of stacks.
> • In F4 use **F4-B1..B5** and modules **8A/8B/9B**.
> • In F5 use **B1..B5** for thematic clarity.

---

## Quick Phase View (durations)

* **Phase 1** (Foundations) · **Q1–Q2** · \~6 months
* **Phase 2** (Applied analysis & first execution paths) · **Q3** · \~4 months
* **Phase 3** (Internals & userland/kernel intro) · **Q4** *(start)*, **Q7–Q9** *(continuation)* · \~12–14 effective months (with a pause)
* **Phase 4** (Evasion, Persistence, C2 + Blue) · **Q10–Q12** · \~12 months
* **Phase 5** (Kernel/Firmware/UEFI/Boot) · **Q13–Q14** · \~8 months

> **TOCD pause:** 2026-09-14 → 2027-08-02 (Bug Bounty + University; BackLogs 6–8 h/week).

---

## Q1 — 2025-08-14 → 2025-11-30

**Phase 1 (start)**

* **0B01 — Linux/CLI/Bash & Ecosystem · 1 stack**
  Stacks/topics: FHS, permissions (chmod/ACL), pipelines (grep/sed/awk), backups/rsync, processes/signals, basic networking, apt/dpkg, minimal OPSEC.
* **1B01 — Toolchain, Debugging & VCS · 1 stack**
  Stacks/topics: Git/PRs/hooks, Make/CMake, binutils, compiler flags, sanitizers, gdb/lldb, strace/ltrace, perf.

## Q2 — 2025-12-01 → 2026-02-07

**Phase 1 (closure)**

* **2B01 — Systems C I (start) · 1 stack**
  Pointers/ownership, safe strings, I/O (stdio vs syscalls), mmap/buffers.
* **3B01 — Systems C I (wrap-up) · 1 stack**
  Testing/coverage, light fuzzing, sockets (blocking/non-blocking).
* **4B01 — x86\_64/ABI/ASM · 1 stack**
  SysV calling convention, stack frames, syscalls, C↔asm, benchmarks.
* **5B01 — Linking/Loading (ELF, PLT/GOT, LD\_PRELOAD) · 1 stack**
  ELF headers/relocs/symbols, shared libs/visibility, hooks via `LD_PRELOAD`, rpath/runpath.

## Q3 — 2026-04-01 → 2026-07-31

**Phase 2 (complete)**

* **0B04 — Applied Reversing I · 4 stacks**
  Static (strings/CFG/calling conv), dynamic (x64dbg/WinDbg), basic anti-analysis, **single-layer unpack** + minimal IAT, support scripting (Python).
* **1B04 — Deep PE & In-Memory Loaders · 4 stacks**
  PE headers/relocs/TLS, local loader (benign shellcode), basic manual map, validation (PE-sieve/Process Hacker).
* **2B04 — Userland Paths & Modern Mitigations · 4 stacks**
  CRT+LoadLibrary, APC, hollowing (lab), DEP/ASLR/CFG, dynamic resolution.
* **EX0B01 — Express Module F2** (tools & harness).
* **3B02 — Bridge F2→F3 · 2 stacks** (evidence packages + F3 warm-up).

## Q4 — 2026-08-01 → 2026-11-30

**Phase 3 (start, through 2026-09-14)**

* **0B04 — Process & Memory Internals (userland, Win/ELF) · 4 stacks**
  PEB/TEB, **region-map**, modules/heaps, methodology/evidence.
* **1B03 — Userland Exploitation I (stack + basic ROP) · 3 stacks**
  Lab-vulnerable case, gadget hunting/ROP intro, mitigations (DEP/ASLR).
* **EX0B01 — Bug Bounty Prep** (playbook/evidence).

> **TOCD pause:** 2026-09-14 → 2027-08-02 (BackLogs).

## Q5 — 2026-12-01 → 2027-03-31

**TOCD pause (Bug Bounty + University)** · BackLogs (reinforcement).

## Q6 — 2027-04-01 → 2027-07-31

**TOCD pause (Bug Bounty + University)** · BackLogs (reinforcement).

## Q7 — 2027-08-03 → 2027-11-30

**Phase 3 (continuation)**

* **0B04 — Advanced Windows Internals (MM/OBJ/ETW/APC) · 4 stacks**
  VADs/**region-map**, Object Manager/**handle-map**, threads/APC, minimal ETW.

## Q8 — 2027-12-01 → 2028-03-31

**Phase 3 (continuation)**

* **1B03 — Userland Exploitation II (info-leak + ROP/JOP Win/Linux) · 3 stacks**
  Leak+ROP (Windows), leak+chain (Linux mprotect/eq), harness/telemetry.
* **2B03 — Heap Exploitation (LFH vs glibc) · 3 stacks**
  UAF/overwrite (Windows), tcache/fastbin (Linux), mitigations.

## Q9 — 2028-04-01 → 2028-07-31

**Phase 3 (closure)**

* **3B03 — Kernel (Windows) fundamentals + local elevation (lab) · 3 stacks**
  KD/IOCTL/IRP, RW primitive, safe VM elevation.
* **4B02 — F3-CAP (userland → SYSTEM) · 2 stacks**
  Integrated PoC + technical defense.

## Q10 — 2028-08-01 → 2028-11-30

**Phase 4 (start)**

* **8A — Initial Access & Covert Delivery** (maldocs, LNK/HTA/JS, AMSI, LOLBins/WMI).
* **8B — Minimal Blue Track** (Sysmon/ETW, YARA/Sigma, KQL).
* **F4-B1 — Evasion I** (anti-analysis, hash-based resolution, string/CFG obfuscation, basic syscalls).

## Q11 — 2028-12-01 → 2029-03-31

**Phase 4 (continuation)**

* **F4-B2 — Evasion II** (APC early-bird, thread-less, module stomping, PPID spoof).
* **9B — Implant Crypto & Packer v2** (AEAD, rotation, light mutation).
* **F4-B3 — Cross-platform Persistence** (Win/Linux/macOS).

## Q12 — 2029-04-01 → 2029-07-31

**Phase 4 (closure)**

* **F4-B4 — Covert C2 & Traffic Profiling** (realistic profile, 72 h).
* **F4-B5 — Covert Operations (lab)** (5-task playbook + blue evaluation).
* **F4-CAP — Integrated Operation (96 h)**.

> **F4 Extensions (optional):** **12A** macOS + EndpointSecurity · **12B** Linux EDR/eBPF · **12C** Android + Frida · **12D** Hardware RE basics · **12E** Bus sniffers & FW pipeline · **12F** Glitching/FPGA lite.
> **Express Module:** **OPSEC/Legal** (3–5 days).

## Q13 — 2029-08-01 → 2029-11-30

**Phase 5 (start)**

* **B1 — Linux Kernel (LKMs, kprobes/ftrace) · themed stacks**
  Kbuild/Kconfig, didactic instrumentation, /proc/sysfs metrics.

## Q14 — 2029-12-01 → 2030-03-31

**Phase 5 (closure)**

* **B2 — Windows Kernel (WDM/WDF, IOCTL/IRP, callbacks)**
* **B3 — Rootkit-style PoCs (lab, reversible & detectable)**
* **B4 — UEFI/OVMF (DXE) & firmware analysis**
* **B5 — Bootflow & Secure Boot (comparative)**
* **F5-CAP — Kernel+firmware chain with technical defense**

---

### Notes

* Each **Block** closes with **PBR + PAD** (integrated mission) and **reproducible evidence**.
* **Stacks** list the main thematic axes per block (high level).
* Dates are reference frames; deliverables do not change with minor calendar shifts.
