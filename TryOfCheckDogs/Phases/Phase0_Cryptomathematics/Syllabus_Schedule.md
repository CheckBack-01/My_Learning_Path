
# Phase 0 — Applied Cryptomathematics (Running in parallel with Phase 1)

**Syllabus & Schedule (Quarters · Blocks · Stacks)**

**Coverage:** 2025-08-21 → \~2025-10-05
**Cadence:** **1 h/day** (Mon–Sat) · \~6 h/week
**Methodology:** **PBR** (reproducible labs) + **PAD** (*Practical Aptitude Drill*: block-integrated mission) · Lab-only (OPSEC/Legal)
**Global Outcomes (F0):** practical mastery of **base conversions** (bin/dec/hex, two’s complement), **modular arithmetic** (operations, inverses, Fermat in practice), essentials of **number theory** (primes, gcd/lcm, factorization) to build crypto intuition, and **minimal linear algebra** for block representations (**Hill-lite**). All deliverables reproducible with a single script and disciplined evidence (`evidence/` with logs, hashes, manifest).

---

## Quarter Map (high level)

* **Q0 (2025-08-21 → 2025-10-05):** `B0M1` Numbers & Bases · `B0M2` Modular Arithmetic & Cryptography · `B0M3` Matrices & Cipher (Hill-lite) · `B0M4` Global PAD — Cryptology Lite

> **Express (parallel):** **F0-Express — Evidence & Scripts Harness** (one-command runner, logs/hashes, `gpg` sealing). Check-ins at the end of each block.

---

## Q0 — Detailed Schedule

### `B0M1` Numbers & Bases (10 class days · \~10 h)

**Goal:** base systems, powers of two, positional representation, conversions (2/10/16), two’s complement.

|   Stack | Topic Cluster (examples)                                                   | Est. Hours | Key Tools                   | Assignment (PBR) · Due                                                   |
| ------: | -------------------------------------------------------------------------- | ---------: | --------------------------- | ------------------------------------------------------------------------ |
| **0.1** | basic operations; commutative/associative/distributive laws; powers of two |         4h | bash, `bc`, `printf`, `xxd` | —                                                                        |
| **0.1** | positional value; **bin/dec/hex** conversions                              |         4h | bash/python                 | **PBR-B0M1-1**: conversion toolkit + tests · **Due:** **Sun 2025-08-31** |
| **0.1** | **two’s complement** and signed representation                             |         2h | python, notes               | —                                                                        |

**PAD (micro):** short justification of methods and edge cases (overflow, sign). **Date:** **Mon 2025-09-01**.

---

### `B0M2` Modular Arithmetic & Cryptography (10 class days · \~10 h)

**Goal:** congruence and operations mod n, modular inverses, **Fermat (operational)**, crypto-motivated drills.

|   Stack | Topic Cluster (examples)                                                | Est. Hours | Key Tools             | Assignment (PBR) · Due                                                        |
| ------: | ----------------------------------------------------------------------- | ---------: | --------------------- | ----------------------------------------------------------------------------- |
| **0.2** | definition of **modulus** & congruence; properties of +/−/× under mod n |         4h | python (`modtool.py`) | —                                                                             |
| **0.2** | modular inverses (extended gcd); Fermat’s little theorem in practice    |         4h | python, `bc`          | **PBR-B0M2-1**: inverse/mod drills + unit tests · **Due:** **Sun 2025-09-14** |
| **0.3** | primes & quick checks; toy key-generation scenarios                     |         2h | bash/python           | —                                                                             |

**PAD (micro):** mini write-up mapping each drill to a crypto use case. **Date:** **Mon 2025-09-15**.

---

### `B0M3` Matrices, Blocks & Cipher (8 class days · \~8 h)

**Goal:** vectors/matrices, dot product, matrix ops in Python/NumPy, **Hill-cipher-lite** end-to-end.

|   Stack | Topic Cluster (examples)                                         | Est. Hours | Key Tools    | Assignment (PBR) · Due                                                |
| ------: | ---------------------------------------------------------------- | ---------: | ------------ | --------------------------------------------------------------------- |
| **0.4** | vectors & matrices; notation; small integer matrices             |         3h | python/NumPy | —                                                                     |
| **0.4** | **Hill-lite**: encode/decode block messages; invertibility mod m |         5h | python/NumPy | **PBR-B0M3-1**: `hillcipher.py` + tests · **Due:** **Sun 2025-09-28** |

**PAD (micro):** correctness proof sketch (determinant/invertibility). **Date:** **Mon 2025-09-29**.

---

### `B0M4` Global PAD — Cryptology Lite (6 class days · \~6 h)

**Goal:** integrated mission: **binarize → modularize → encrypt** using your toolchain; full evidence.

|   Track | Mission Elements (examples)                                                        | Est. Hours | Evidence & Tools                  | Deliverable · Date                                      |
| ------: | ---------------------------------------------------------------------------------- | ---------: | --------------------------------- | ------------------------------------------------------- |
| **PAD** | convert dataset across bases; compute checksums; build modular keys; run Hill-lite |         6h | `pbr/run.sh`, `gpg`, logs, hashes | **PAD-F0**: `mission.asc` + report · **Sun 2025-10-05** |

---

## Express Module (parallel) — **F0-Express: Evidence & Scripts Harness**

**Check-ins:** end of each block (`B0M1` → `B0M4`).
**Deliverable:** one-command runner (`pbr/run.sh`), `evidence/` with `run.log`, `checksums.txt`, `manifest.json`, `screens/`, and a signed tag per block (e.g., `vF0-B0M1`). Final sign-off: **Sun 2025-10-05**.

---

## Grading & Milestones (Phase 0)

* **PBRs:** most Sundays (see tables).
* **PADs (Exams):** micro-PADs per block; final PAD on **2025-10-05**.
* **Phase 0 Final Sign-off:** **2025-10-05** — all PBR/PAD complete, evidence reproducible, OPSEC/Legal applied.
* **Rubric:** A/B/C/Redo per block (conversion toolkit; modular drills; Hill-lite; integrated mission with signed evidence).

---

### Notes

* Dates are anchor points; small shifts won’t alter deliverables.
* All work is **benign** and in an **isolated VM**, with snapshots and **rollback**.
* Codes follow F0 nomenclature (`B0M1…B0M4`); PAD = **block-integrated mission**.
