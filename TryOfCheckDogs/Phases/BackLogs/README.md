
# BackLogs — Segment 2 (Advanced F3 + F4 Pre-flight)

**Mini-challenge pack for technical continuity (v1.0)**

> Usage: weekly reinforcement (6–8 h) from **2027-08-03 → 2028-03-31**.
> Scope: **Phase 3 (advanced)** content, selective reinforcements from **late Phase 2**, and **pre-flight into Phase 4 (8A/8B)**.
> Format: 15–60 min katas with acceptance criteria and minimal evidence (**PBR-lite + PAD-lite**).

---

## Rules of the game

* **Timeboxing:** S = 15 min, M = 30 min, L = 45 min, XL = 60 min. If it doesn’t land, log the blocker and move on.
* **Minimal evidence** (per challenge): script/command or PoC, output/artifact, 1–3 screenshots, 3–5 lines of lessons learned.
* **Repository:** everything goes under `backlogs/YY-WW/<challenge-ID>/` with a short `README.md` and optional `Makefile`.
* **OPSEC/Legal:** isolated lab, self-built binaries or didactic samples; never third-party executables outside the lab.

## Biweekly cadence (template)

* **Week A (4 h):** 1 challenge from each category: CLI, Toolchain, C, ELF/PE.
* **Week B (4 h):** Reversing/Unpack, Loaders, Internals/ROP, Open review.
* Close each week with **one single report** `Wxx-summary.md` (max 200 words).

---

# Mini-challenge catalog

> Each entry includes: **ID** · **Title** · **Effort** · **Prereq** · **Task** · **Acceptance criteria** · **Deliverables**

## 1) Linux/CLI/Bash

**B1-CLI-09** · `journalctl` → per-unit CSV · **S**
Prereq: journalctl/grep.
Task: extract events from 2 services and produce `unit,severity,count`.
Acceptance: reproducible CSV with `make run`.
Deliverables: script + CSV.

**B1-CLI-10** · `awk` join of 2 CSVs · **S**
Prereq: awk/sort.
Task: join `modules.csv` and `regions.csv` on `pid`.
Acceptance: aligned and deduplicated rows.
Deliverables: script + out.

**B1-CLI-11** · `inotifywait` watchdog · **M**
Prereq: inotify-tools.
Task: restart a dummy process when `config.cfg` changes.
Acceptance: event log with timestamps.
Deliverables: script + log.

**B1-CLI-12** · `rsync` with checksum verification · **M**
Prereq: rsync/shasum.
Task: incremental backup with `--checksum` and safe `--delete`.
Acceptance: 3 runs show only actual changes.
Deliverables: script + hash listing.

**B1-CLI-13** · `xargs -P` bounded parallelism · **S**
Task: process 100 files with a limit of 4 concurrent jobs.
Acceptance: no races and a final summary.
Deliverables: script + out.

**B1-CLI-14** · diff with date masking · **M**
Task: generate a diff that ignores timestamps `YYYY-MM-DD HH:MM`.
Acceptance: report with 3 cases.
Deliverables: script + fixtures.

## 2) Toolchain/Debugging

**B2-TOOL-06** · GDB init with useful commands · **S**
Task: `.gdbinit` with pretty-printing, conditional break, and memory dump.
Acceptance: demo on a lab binary.
Deliverables: file + notes.

**B2-TOOL-07** · `perf record`/`report` basics · **M**
Prereq: perf.
Task: capture hot paths of a C utility.
Acceptance: top-5 symbols with percentages.
Deliverables: script + PNG.

**B2-TOOL-08** · Cross sanitizers (ASan/UBSan) · **M**
Task: enable both and document 1 bug found.
Acceptance: clean logs after the fix.
Deliverables: diff + log.

**B2-TOOL-09** · Reproducible core dumps · **M**
Task: configure ulimit and collect a stable backtrace.
Acceptance: correct symbols and root cause.
Deliverables: core + commands.

**B2-TOOL-10** · `strace` syscall filters · **S**
Task: measure only `openat/execve` and count occurrences.
Acceptance: `syscall,count` table.
Deliverables: out + summary.

## 3) Systems C

**B3-C-08** · Safe `mmap` patcher · **L**
Task: patch bytes at an offset with bounds checks.
Acceptance: hash before/after; rollback.
Deliverables: code + tests.

**B3-C-09** · Robust CLI (getopt) · **M**
Task: implement `-i/-o/-v` flags with clear error reporting.
Acceptance: valid and failing argument tests.
Deliverables: code + tests.

**B3-C-10** · CRC32/xxHash module · **M**
Task: compute file hash in blocks for a large file.
Acceptance: matches a reference tool.
Deliverables: code + log.

**B3-C-11** · `proc/<pid>/maps` region viewer · **M**
Task: map and color types (stack/heap/file).
Acceptance: stable output on 2 processes.
Deliverables: code + screenshots.

**B3-C-12** · TCP client with fine-grained timeouts · **M**
Task: connect, send, and validate `SO_RCVTIMEO/SO_SNDTIMEO`.
Acceptance: clear timeout logs.
Deliverables: code + log.

## 4) x86\_64/ABI/asm

**B4-ASM-04** · `memcpy` SSE vs C (short bench) · **L**
Task: compare an SSE2 asm version with safe C.
Acceptance: chart and conclusions.
Deliverables: asm + bench.

**B4-ASM-05** · Syscall wrapper with errno · **M**
Task: `gettimeofday` or similar, no libc.
Acceptance: valid errno on simulated failure.
Deliverables: code + README.

**B4-ASM-06** · Mixed struct passing C↔asm · **M**
Task: verify alignment and SysV ABI.
Acceptance: consistent fields.
Deliverables: code + tests.

## 5) ELF/PE/Linking

**B5-ELF-06** · Relocs and imports (ELF) · **L**
Task: list relocation entries and affected symbols.
Acceptance: evidence with `readelf -r`.
Deliverables: tool + screenshots.

**B5-ELF-07** · `LD_DEBUG` analysis · **M**
Task: compare runtime resolution for 3 symbols.
Acceptance: before/after table.
Deliverables: script + notes.

**B5-PE-08** · Forwarded imports (PE) · **M**
Task: detect and resolve forwarded imports.
Acceptance: demo with a lab DLL.
Deliverables: script + evidence.

**B5-PE-09** · TLS callbacks execution order · **M**
Task: enumerate callbacks and show their firing.
Acceptance: debugger screenshots.
Deliverables: script + PNG.

## 6) Reversing/Unpack

**B6-REV-05** · API hashing (XOR/ROL) · **S**
Task: identify the scheme and decode 10 names.
Acceptance: clean list.
Deliverables: script + out.

**B6-REV-06** · TE/overlay detector · **M**
Task: flag the presence of a TE header or overlay in PE files.
Acceptance: 3 samples with verdicts.
Deliverables: tool + cases.

**B6-REV-07** · Partial IAT repair · **L**
Task: rebuild essential imports after a dump.
Acceptance: loads in Ghidra without major errors.
Deliverables: dump + guide.

**B6-REV-08** · Basic anti-debug bypass (PEB) · **M**
Task: bypass `BeingDebugged` and trivial timing checks.
Acceptance: stable session in x64dbg.
Deliverables: notes + symbols.

## 7) Loaders/Userland execution

**B7-LOD-05** · Local APC (early-bird) · **L**
Task: benign demo in your own process.
Acceptance: observable event and cleanup.
Deliverables: code + logs.

**B7-LOD-06** · Manual map with relocations · **XL**
Task: map a minimal DLL with relocs and limited imports.
Acceptance: export executes and rollback works.
Deliverables: code + evidence.

**B7-LOD-07** · CLI technique selector (v2) · **L**
Task: CRT+LL / APC / additional stub.
Acceptance: comparable logs.
Deliverables: binary + README.

**B7-LOD-08** · Comparative traces v2 · **M**
Task: measure artifacts vs baseline (8B-like).
Acceptance: table and conclusions.
Deliverables: report.

## 8) Internals/ROP (educational)

**B8-ROP-04** · Didactic info-leak · **L**
Task: leak a pointer in a lab app and compute the base.
Acceptance: correct offsets without crashing.
Deliverables: PoC + screenshots.

**B8-ROP-05** · `mprotect`/`VirtualProtect` call chain · **L**
Task: ROP chain that adjusts permissions in a dummy region.
Acceptance: verification in the debugger.
Deliverables: PoC + logs.

**B8-ROP-06** · ret2libc (Linux parallel) · **L**
Task: minimal chain in a lab binary.
Acceptance: observable and safe effect.
Deliverables: write-up.

**B8-ROP-07** · Controlled heap UAF (Win) · **XL**
Task: didactic PoC that controls a function pointer.
Acceptance: stable execution in a VM.
Deliverables: code + evidence.

**B8-ROP-08** · Hardening post-mortem · **M**
Task: recompile a mitigated binary that neutralizes your PoC.
Acceptance: demo of neutralization.
Deliverables: diff + tests.

---

## PAD-lite (template)

```
# Challenge <ID> — <Title>
## Objective
...
## Key steps
- ...
## Evidence
- out.txt / screenshot(s)
## Lessons
- 3–5 bullets
```

## Control metrics (weekly)

* Challenges completed (target: 4/week).
* Effective time (target: 6–8 h/week).
* Open/closed blockers.
* “Signal vs noise” in PoCs (when applicable).

## Cycle close-out (biweekly)

* `Wxx-summary.md` with: what worked, what didn’t, the next 4 challenges, and 1 automation idea for tooling.

---

### Final note

This pack does NOT replace the TOCD progression. It keeps your hands, memory, and judgment sharp through **Advanced F3 → pre-F4**, setting up a cleaner entry into 8A/8B without opening new fronts outside the lab. Adjust difficulty based on fatigue and academic load.

