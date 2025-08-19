
# Phase 1 — ENIAC (Fundamentals)

**Scope.** Phase 1 builds low-level fluency in Linux/CLI, a professional toolchain, Systems-C, x86\_64/ABI, and ELF/PLT/GOT with `LD_PRELOAD`. You’ll ship small, verifiable utilities and learn to reason about memory, calling conventions, linking/loading, and basic binary analysis.&#x20;

**Methodology.** Each block closes with **PBR** (reproducible lab) + **PAD** (Practical Aptitude Drill: a scenario-style, **integrated multi-tech mission per block**, with evidence and replication steps). OPSEC/Legal is applied throughout.

**Phase-level outcomes.**
• 8–12 PBRs with their PADs • 1 small system utility in C (generic Makefile + local CI) • 1 simple hexdump/patcher • 1 `LD_PRELOAD` userland hooking demo • Lab logbook + minimal OPSEC checklist.&#x20;

---

## How Phase 1 is organized

**Nomenclature.** Blocks use short codes like `0B01`, where `X` is the zero-based block index and `YY` is the count of stacks inside that block (when applicable).

**Blocks in ENIAC**

### `0B01` — Linux/CLI/Bash & Ecosystem

**Goal.** Operate confidently in the console; manipulate files/text; manage permissions/processes; work safely in an isolated lab.
**Highlights.** FHS & permissions (chmod/ACL), pipes/grep/sed/awk, find/xargs/tar/rsync, ps/kill/nohup/jobs, basic networking, apt/dpkg, lab hygiene.&#x20;
**PBR examples.** Incremental backup with verification; log-processing pipeline to CSV; collaborative ACL lab with tests.&#x20;
**PAD evidence.** VM FHS diagram, permission tables, pipeline flow.&#x20;

### `1B01` — Toolchain, Debugging & VCS

**Goal.** Compile, link, and debug professionally; add diagnostics and measure performance.
**Highlights.** Git workflow, Make/CMake templates, gcc/clang flags, sanitizers, gdb/lldb, strace/ltrace, perf, binutils (readelf/objdump/nm/strings).&#x20;
**PBR examples.** Generic Makefile (`build/test/clean/asan/ubsan`); ASan bug-hunt with core dump; memcpy/memmove micro-benchmark.&#x20;
**PAD evidence.** Failure report (traces, root cause, documented fix); quick guide to your build template.&#x20;

### `2B01–3B01` — Systems C I (two stacks)

**Goal.** Master memory & pointers, low-level I/O, and safe C patterns.
**Highlights.** Pointers/const/restrict/fn-ptrs; structs/unions/bitfields, alignment; malloc/free & ownership; errno & contracts; stdio vs syscalls, buffers, mmap; safe binary parsing; basic sockets; common bug classes & mitigations.&#x20;
**PBR examples.** Custom `hexdump`; mini safe-strings library + tests; mmap-based mini binary viewer.&#x20;
**PAD evidence.** Function specs/contracts/test cases; threat report & mitigations.&#x20;

### `4B01` — x86\_64 Architecture & ABI; Practical Assembly

**Goal.** Understand calling conventions, stack behavior, and syscall invocation.
**Highlights.** SysV x86\_64 CC; prologue/epilogue; stack frames & callee-saved regs; syscalls & errno; inline asm; C↔asm integration; Windows x64 vs SysV (conceptual).&#x20;
**PBR examples.** `memset`/`memcmp` in asm with cross-tests; minimal syscall wrappers (`write`, `getpid`) without libc; mixed C+asm struct passing.&#x20;
**PAD evidence.** ABI notes with stack diagrams; comparative benchmarks.&#x20;

### `5B01` — Linking, Loading & Formats (ELF, PLT/GOT, `LD_PRELOAD`)

**Goal.** See how the loader resolves symbols and how to intercept calls in userland.
**Highlights.** ELF headers/sections vs segments/relocations/symbols; static/dynamic linking, PIC/PIE, PLT/GOT & lazy binding; `ldd`, `patchelf`, `objdump/readelf`; shared libraries & symbol visibility; **`LD_PRELOAD`** hooks; high-level PE vs ELF.&#x20;
**PBR examples.** Minimal ELF parser (sections & symbols); shared-lib hook for `open/fopen`; controlled `rpath/runpath` change with `patchelf`.&#x20;
**PAD evidence.** Linking-architecture report; symbol tables before/after hooking with proof.&#x20;

---

## What you’ll learn (skills & mindset)

* Console mastery (pipes/filters), permissions/ACLs, process & network basics.&#x20;
* A maintainable build/debug toolchain with sanitizers and basic profiling.&#x20;
* Systems-C fluency: memory ownership, safe I/O, contracts, and testing.&#x20;
* x86\_64 calling conventions and practical asm interop.&#x20;
* ELF/linking internals and `LD_PRELOAD`-based hooks.&#x20;

---

## Outcomes & success criteria

* Warning-free builds with `-Wall -Wextra -Werror`; sanitizers & `valgrind` clean in planned scenarios.&#x20;
* Tested utilities (hexdump, parsers, hooks) with reproducible evidence (hashes, logs, env info).&#x20;
* Phase-level grading: **A** = all PBR/PAD complete, clean diagnostics, functional hooking, clear docs, one-command reproducibility.&#x20;

---

## PBR & PAD — how we evaluate

* **PBR (Proof-of-Bounty-Readiness).** A **reproducible lab** with explicit objectives, testable steps, and artifacts (code, logs, screenshots, hashsets).
* **PAD (Practical Aptitude Drill).** A **block-level integrated mission** that exercises multiple techniques you learned in the block. It is evaluative, includes risks/limits, and must be reproducible in your lab.

> Every block closes with **PBR + PAD** and a minimal evidence package.

---

**Ethics & scope.** Lab-only, benign payloads, NAT-only networking, and no third-party systems. See `docs/Opsec_Legal.md` for the full policy.
