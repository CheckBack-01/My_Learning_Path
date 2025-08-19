
# Phase 2 — IBM 1401 (Applied Reversing & Userland Execution)

**Scope.** Phase 2 consolidates applied reversing and the first userland execution paths. You’ll learn to reason about real-world binaries (static/dynamic), manually unpack simple layers, and build **loaders** that execute benign payloads in memory using classic injection techniques, while accounting for modern mitigations.

**Methodology.** Each block closes with **PBR** (reproducible lab) + **PAD** (Practical Aptitude Drill: a scenario-style, **integrated multi-tech mission per block**, with evidence and replication steps). OPSEC/Legal is applied throughout.

**Phase-level outcomes.**
• Reversing report on a real binary (light obfuscation) with a **reproducible unpack**. • A usable **PE parser** and supporting analysis utilities. • A **userland loader** implementing at least two execution techniques. • Intro **process hollowing** PoC in a controlled lab. • Documentation discipline and an evidence pack suitable for future bug bounty work.

---

## How Phase 2 is organized

**Nomenclature.** Blocks use short codes like `0B01`, where `X` is the zero-based block index and `YY` is the count of stacks inside that block (when applicable).

**Blocks in IBM 1401**

### `0B04` — Applied Reversing I: tools, methodology & basic unpacking

**Goal.** Master a static/dynamic pipeline with Ghidra/IDA and x64dbg/WinDbg; spot trivial anti-analysis; perform a **manual unpack** of one layer (e.g., UPX-like) with minimal IAT reconstruction.
**Highlights.** Ghidra/IDA (free), rizin/Cutter, x64dbg/WinDbg; strings/signatures, CFG, calling conventions, struct recovery; breakpoints, memory map, dump & patch, basic relocations; simple anti-debug/time checks and bypasses; **Packers 101** (find OEP, rebuild IAT); Python scripting for decoders/parsers and dump automation.
**PBR examples.** Reversing report for a small sample with obfuscated strings; **manual unpack** of a packed sample with a clean dump and functional IAT; **string/config decoder** script (e.g., XOR/RC4-lite) with unit tests.
**PAD evidence.** Step-by-step methodology, screenshots, pre/post checksums, issues encountered and mitigations; third-party reproducibility via your repo/lab checklist.

### `1B04` — Deep PE, Windows API & in-memory loaders

**Goal.** Understand PE in practice (headers, sections, imports/exports, relocations, TLS) and build **loaders** that run benign payloads in memory, advancing toward **manual mapping** basics.
**Highlights.** DOS/NT headers; sections vs segments; imports/exports; relocations; TLS callbacks; PE vs ELF contrasts. Windows processes/threads/memory: `VirtualAlloc{Ex}`, `WriteProcessMemory`, `Create{Remote}Thread`, `VirtualProtect`. Minimal loader: allocate + copy + protect + controlled jump. **Manual mapping (intro):** DLL load without `LoadLibrary` (selected import resolution, essential relocs, no advanced TLS). Stability concerns: perms, offsets, alignment, silent crashes. Inspection with Process Hacker, PE-bear, PE-sieve.
**PBR examples.** **PE parser** that prints key headers, sections, and imports with a basic integrity check; **local shellcode loader** with error handling and cleanup; **intro manual map** of a tiny DLL and execution of an exported function.
**PAD evidence.** Loader design, memory layout diagrams, risk notes, and test harness with sanitized error handling.

### `2B04` — Userland execution paths & modern mitigations

**Goal.** Implement 2–3 classic injection/execution techniques in userland and understand the effect of **DEP/ASLR/CFG** and handle policies; prepare for Evasion/Obfuscation and the upcoming Initial Access module.
**Highlights.** Classic injection: `CreateRemoteThread + LoadLibrary`. **APC queueing** (incl. early-bird) and synchronization issues. **Process hollowing** (intro) vs module stomping. PPID spoofing and relevant `CreateProcess` options for staged execution in a lab. Light obfuscation: hashed API resolution, hidden strings. Mitigations: DEP/ASLR/CFG, lab AV/signing basics; common detection surfaces. Intro to **syscalls** for basic ops (no unhooking yet).
**PBR examples.** **Mode-switching loader** with CLI-selectable technique (at least CRT+LL and APC) and controlled logging; **hollowing PoC** against a lab binary with evidence and safe reversion; **trace comparison** across techniques under a fixed checklist with documented artifact differences.
**PAD evidence.** Mitigation analysis, detection-surface notes, and an improvement plan feeding into Phase 3 and modules 8A/8B.

---

## What you’ll learn (skills & mindset)

* Applied reversing with a reproducible static/dynamic workflow and basic unpacking.
* Practical PE knowledge and in-memory execution via loaders and intro manual mapping.
* Multiple userland execution paths, their artifacts, and mitigation-aware design.
* Documentation habits that produce third-party-reproducible evidence suitable for bounty contexts.

---

## Outcomes & success criteria

* Working **unpacked** binary with a functional IAT and analyzable static profile.
* A usable **PE parser** and tooling that accelerates your analysis.
* A **stable loader** that executes a benign payload and supports ≥2 techniques.
* A **process hollowing** PoC that is reproducible and safely reversible in lab conditions.
* Phase-level grading: **A** = clean unpack + useful PE parser + ≥2 loader techniques + stable hollowing PoC + clear, one-command reproducibility; **B** = ≥80% PBR/PAD, one unstable technique or incomplete parser; **C** = ≥60% with partial reproducibility; **Redo** = <60% or severe instability.

---

## PBR & PAD — how we evaluate

* **PBR (Proof-of-Bounty-Readiness).** A **reproducible lab** with explicit objectives, testable steps, and artifacts (code, logs, screenshots, hashsets).
* **PAD (Practical Aptitude Drill).** A **block-level integrated mission** that exercises multiple techniques you learned in the block. It is evaluative, includes risks/limits, and must be reproducible in your lab.

> Every block closes with **PBR + PAD** and a minimal evidence package.
