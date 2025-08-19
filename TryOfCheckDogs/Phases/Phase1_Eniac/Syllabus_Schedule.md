
# Phase 1 — ENIAC (Fundamentals)

**Syllabus & Schedule (Quarters · Blocks · Stacks)**

**Coverage:** 2025-08-14 → \~2026-02
**Cadence:** \~30 h/week (5 h/day, Mon–Sat)
**Methodology:** **PBR** (reproducible labs) + **PAD** (*Practical Aptitude Drill*: block-integrated mission) · Lab-only (OPSEC/Legal)
**Global Outcomes (F1):** 8–12 PBRs + PADs, 1 system utility in C, simple hexdump/patcher, `LD_PRELOAD` hook demo, lab logbook & minimal OPSEC checklist.&#x20;

---

## Quarter Map (high level)

* **Q1 (2025-08-14 → 2025-11-30):** `0B01` Linux Fundamentals, `1B01` Toolchain & Debugging
* **Q2 (2025-12-01 → 2026-02-28):** `2B01` Systems C I (start), `3B01` Systems C I (wrap-up), `4B01` x86\_64/ABI/ASM, `5B01` Linking/ELF/PLT/GOT/`LD_PRELOAD`

> **Express Module (parallel):** **F1-Express — Minimal Lab OPSEC** — distributed check-ins at each block end.&#x20;

---

## Q1 — Detailed Schedule

### `0B01` Linux Fundamentals (6 weeks · \~180 h total)

**Goal:** Console fluency; file/text pipelines; permissions; processes; basic network; packaging; lab hygiene.&#x20;

**Stacks & Topics (with hours and assignments)**

| Stack                        | Topic Cluster (examples)                                         | Est. Hours | Key Tools                    | Assignment (PBR) · Due                                                           |
| ---------------------------- | ---------------------------------------------------------------- | ---------: | ---------------------------- | -------------------------------------------------------------------------------- |
| **FHS & Permissions**        | FHS, users/groups, `chmod/chown/umask`, ACLs                     |       24 h | coreutils, `getfacl/setfacl` | **PBR-0B01-1**: Collaborative ACL lab · **Due:** Sun **2025-08-31**              |
| **Text Pipelines**           | pipes, redirection, `grep/sed/awk`, regex, `cut/sort/uniq/tr/wc` |       30 h | GNU tools                    | **PBR-0B01-2**: Log pipeline + CSV summary · **Due:** Sun **2025-09-07**         |
| **File Management**          | `find/xargs`, `tar/gzip`, `rsync`, rotations                     |       18 h | `find`, `rsync`              | **PBR-0B01-3**: Incremental backup w/ verification · **Due:** Sun **2025-09-14** |
| **Processes & Signals**      | `ps/top/htop`, `kill`, nice/renice, jobs/bg/fg, `nohup`          |       18 h | proc tools                   | Checkpoint quiz (theory) · **2025-09-18**                                        |
| **Basic Networking**         | `ip/route`, `ss`, `ping/traceroute`, `/etc/hosts`, DNS           |       24 h | iproute2                     | Mini-lab: network quick-survey · **Due:** **2025-09-25**                         |
| **Packaging (Deb/Ubuntu)**   | repos, `apt/dpkg`, version pinning                               |       12 h | apt/dpkg                     | –                                                                                |
| **Lab Hygiene (OPSEC-lite)** | snapshots, metadata, timestamps                                  |       12 h | VM mgr                       | **Express OPSEC Check-in #1** · **2025-09-27**                                   |

**PAD (Exam) — `PAD-0B01`**
**Window:** **2025-09-28 → 2025-10-01** · **Deliverable:** one integrated mission (pipeline + permissions + backup) with reproducible evidence and short defense notes.

---

### `1B01` Toolchain, Debugging & Version Control (4 weeks · \~120 h total)

**Goal:** Professional build/debug profile; diagnostics; performance.&#x20;

| Stack                    | Topic Cluster                                             | Est. Hours | Key Tools     | Assignment (PBR) · Due                                                                   |
| ------------------------ | --------------------------------------------------------- | ---------: | ------------- | ---------------------------------------------------------------------------------------- |
| **Git & Workflow**       | branches, local PRs, hooks, semantic tags                 |       18 h | git           | Repo hygiene checklist · **2025-10-08**                                                  |
| **Make/CMake**           | targets/deps/vars, reusable templates                     |       24 h | make/cmake    | **PBR-1B01-1**: Generic Makefile (build/test/asan/ubsan/clean) · **Due:** **2025-10-12** |
| **Compilers & Flags**    | gcc/clang, `-O{0..3}`, `-g`, `-Wall -Wextra -Werror`, LTO |       18 h | gcc/clang     | –                                                                                        |
| **Sanitizers**           | ASan/UBSan/Leak, assertions                               |       18 h | `-fsanitize`  | **PBR-1B01-2**: Memory bug-hunt + core dump analysis · **Due:** **2025-10-19**           |
| **Debug/Tracing**        | `gdb/lldb`, `strace/ltrace`, core files                   |       24 h | gdb/lldb      | –                                                                                        |
| **Profiling & Binutils** | `perf`, `time`, `readelf/objdump/nm/strings`              |       18 h | perf/binutils | **PBR-1B01-3**: memcpy/memmove micro-benchmark · **Due:** **2025-10-26**                 |

**PAD (Exam) — `PAD-1B01`**
**Date:** **2025-10-30** · **Deliverable:** write-up + quick demo of your build template, failure analysis, and performance notes.

**Q1 Midterm Checkpoint (non-graded):** **2025-11-05** — short oral defense (10–12 min) on 0B01/1B01 takeaways + OPSEC mini-audit.

---

## Q2 — Detailed Schedule

### `2B01` Systems C I — Part A (4 weeks · \~120 h total)

**Goal:** Pointers & memory, safe I/O, mmap, binary parsing foundations.&#x20;

| Stack                     | Topic Cluster                                                           | Est. Hours | Assignment (PBR) · Due                                                                      |
| ------------------------- | ----------------------------------------------------------------------- | ---------: | ------------------------------------------------------------------------------------------- |
| **Pointers & Layout**     | pointers, `const/restrict`, structs/unions/bitfields, alignment/padding |       24 h | –                                                                                           |
| **Dynamic Memory**        | `malloc/calloc/realloc/free`, ownership, simple arenas                  |       24 h | –                                                                                           |
| **I/O & mmap**            | stdio vs syscalls (`open/read/write`), buffers, `mmap`                  |       30 h | **PBR-2B01-1**: custom **hexdump** (offset + ASCII) · **Due:** **2025-12-21**               |
| **Binary Parsing (safe)** | headers, checks, error contracts                                        |       24 h | **PBR-2B01-2**: mini binary viewer (header + sections via `mmap`) · **Due:** **2026-01-04** |
| **Error Handling**        | `errno`, contracts, preconditions                                       |       18 h | –                                                                                           |

**PAD (Exam) — `PAD-2B01-A`**
**Date:** **2026-01-06** · **Deliverable:** specs + test matrix + threat report for your utilities.

---

### `3B01` Systems C I — Part B (4 weeks · \~120 h total)

**Goal:** Safe string subset, sockets intro, tests & fuzzing light.&#x20;

| Stack                     | Topic Cluster                             | Est. Hours | Assignment (PBR) · Due                                                     |
| ------------------------- | ----------------------------------------- | ---------: | -------------------------------------------------------------------------- |
| **Safe Strings (subset)** | `x_strlcpy/strnlen_s` style + tests       |       30 h | **PBR-3B01-1**: safe string lib + >80% coverage · **Due:** **2026-01-18**  |
| **Sockets Intro**         | TCP/UDP; blocking vs non-blocking         |       24 h | **PBR-3B01-2**: minimal TCP client (timeouts OK) · **Due:** **2026-01-25** |
| **Testing & Fuzzing**     | unit tests; honggfuzz/AFL (20-min runs)   |       30 h | **PBR-3B01-3**: parser fuzz pass (no crashes) · **Due:** **2026-02-01**    |
| **Security Pitfalls**     | bounds, off-by-one, fmt, UAF, double-free |       24 h | –                                                                          |
| **Docs & Contracts**      | function specs, contracts, cases          |       12 h | –                                                                          |

**PAD (Exam) — `PAD-3B01`**
**Date:** **2026-02-03** · **Deliverable:** consolidated docs + test/evidence pack.

---

### `4B01` x86\_64 Architecture & ABI; Practical Assembly (4 weeks · \~120 h total)

**Goal:** Calls, stack discipline, syscalls, C↔asm integration, ABI contrasts.&#x20;

| Stack                          | Topic Cluster                              | Est. Hours | Assignment (PBR) · Due                                                             |
| ------------------------------ | ------------------------------------------ | ---------: | ---------------------------------------------------------------------------------- |
| **SysV ABI & Stack**           | registers, prologue/epilogue, nested calls |       24 h | –                                                                                  |
| **Syscalls & errno**           | numbers, `syscall`, errors/`errno`         |       24 h | **PBR-4B01-1**: syscall wrapper (`write/getpid`) no libc · **Due:** **2026-02-10** |
| **C ↔ asm Integration**        | inline asm; structs by value               |       30 h | **PBR-4B01-2**: mixed C+asm passing structs · **Due:** **2026-02-15**              |
| **Mem Routines in asm**        | `memset/memcmp` impl + cross-tests         |       30 h | **PBR-4B01-3**: asm vs C benchmarks · **Due:** **2026-02-20**                      |
| **ABI Contrast (Win vs SysV)** | conceptual differences                     |       12 h | –                                                                                  |

**PAD (Exam) — `PAD-4B01`**
**Date:** **2026-02-22** · **Deliverable:** ABI notes (stack diagrams) + comparative benches.

---

### `5B01` Linking, Loading & Formats (ELF, PLT/GOT, `LD_PRELOAD`) (4 weeks · \~120 h total)

**Goal:** Loader symbol resolution and userland interception.&#x20;

| Stack                      | Topic Cluster                                  | Est. Hours | Assignment (PBR) · Due                                                                |
| -------------------------- | ---------------------------------------------- | ---------: | ------------------------------------------------------------------------------------- |
| **ELF Basics**             | headers, sections vs segments, relocs, symbols |       30 h | **PBR-5B01-1**: minimal **ELF parser** (sections + symbols) · **Due:** **2026-02-26** |
| **Linking (PIC/PIE)**      | static/dynamic, PLT/GOT, lazy binding          |       24 h | –                                                                                     |
| **Shared Libs**            | building `.so`, symbol visibility              |       18 h | **PBR-5B01-2**: `LD_PRELOAD` hook for `open/fopen` · **Due:** **2026-02-28**          |
| **Tooling**                | `ldd`, `patchelf`, `objdump/readelf`           |       24 h | **PBR-5B01-3**: manual `rpath/runpath` tweak (PoC) · **Due:** **2026-03-02**          |
| **PE vs ELF (high level)** | future prep                                    |       12 h | –                                                                                     |

**PAD (Exam) — `PAD-5B01`**
**Date:** **2026-03-04** · **Deliverable:** linking architecture report + symbol tables before/after hooking with evidence.

---

## Express Module (parallel) — **F1-Express: Minimal Lab OPSEC**

**Check-ins:** end of each block (`0B01`, `1B01`, … `5B01`)
**Deliverable:** signed OPSEC checklist applied across F1 repos (final sign-off **2026-03-06**).&#x20;

---

## Grading & Milestones (Phase 1)

* **PBRs:** weekly, due most Sundays (see tables).
* **PADs (Exams):** at block ends (dates above).
* **Phase 1 Final Sign-off:** **2026-03-08** — all PBR/PAD complete, evidence reproducible, OPSEC checklist signed, one-command lab repro OK.
* **Rubric:** A/B/C/Redo per F1 spec (sanitizers clean, tests present, docs clear).&#x20;

---

### Notes

* Dates are planned anchors; minor shifts won’t alter deliverables.
* All work is **lab-only**, with **benign** payloads, snapshots, and **reproducible** evidence.
* Block codes follow F1 nomenclature (`0B01`…`5B01`); PAD = **block-integrated mission**.
