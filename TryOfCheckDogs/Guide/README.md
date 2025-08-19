
# Guide — Recruiter Overview (TOCD / My_Learning_Path)

**What this is**  
Public repository for **TOCD (Try Of Check Dogs)** — a self-directed path in **Reverse Engineering** and **Malware Development** focused on **evasion, persistence, and C2**. All work is **lab-only** and professionally documented.

**Who should read this**  
Recruiters and hiring managers who need a fast, high-level understanding of the repo’s scope, organization, metrics, and evidence without browsing everything.

---

## 1) 30-second summary
- Multi-year path using **PBR** (reproducible labs) + **PAD** (analysis & docs).
- Realistic progression: **Phase 1 (Fundamentals)** → **Phase 2 (Reversing/Loaders)** → **Phase 3 (Internals & Exploits)** → **Phase 4 (Evasion/Persistence/C2)** → **Phase 5 (Kernel/UEFI)**.
- Every block ships **code, evidence, and documentation** you can verify.
- **Ethics/OPSEC:** executed **only in VMs** with **benign content**; never on third-party systems.

---

## 2) How it’s organized (top → bottom)
**Phase → Block → Stack → PBR/PAD**

- **Phase (F1–F5):** macro objective (e.g., F1 fundamentals, F2 reversing, F3 userland exploitation, F4 evasion/C2, F5 kernel/UEFI).  
- **Block (B1, B2, …):** topic within a phase (e.g., “PE & loaders”).  
- **Stack:** sequential sub-topics inside a block.  
- **PBR — Proof-of-Bounty-Readiness:** a **reproducible** lab with clear goals and evidence.  
- **PAD:** the technical write-up for that PBR (method, environment, results, limits, reproduction steps).

> Typical path: `PhaseX_*/B*/` → `labs/` (code) · `evidence/` (artifacts) · `docs/` (PAD).

---

## 3) Core glossary (short definitions)
- **PBR:** lab with verifiable steps and a **reproducible outcome** (datasets/tests included).  
- **PAD:** technical report for the PBR (methodology, risks, reproducibility, “how to reproduce”).  
- **Encrypted Mission:** practice with **GPG-encrypted** instructions; decrypted **only inside the VM**.  
- **Capstone:** integrative exercise chaining multiple techniques with a technical defense.  
- **BackLogs:** short weekly katas to keep skills fresh during lower-bandwidth periods.  
- **Evidence:** logs, screenshots, hashes, environment versions, and test results.

---

## 4) Suggested reading order (overview)
1. **F1 — Fundamentals:** Linux/CLI, toolchain, C/ASM, ELF/linking.  
2. **F2 — Applied analysis:** static/dynamic reversing, basic unpack, **PE & loaders**, classic injection.  
3. **F3 — Internals & Exploits:** PEB/TEB, regions, **ROP/JOP**, heap (Win/Linux), driver RW (lab).  
4. **F4 — Evasion/Persistence/C2:** anti-analysis, dynamic resolution, **persistence** (Win/Linux/macOS), C2 profiling, **Blue-team validation**.  
5. **F5 — Kernel/UEFI:** LKMs/kprobes, benign Windows driver, **DXE** on OVMF, Secure Boot comparison.

---

## 5) What a recruiter will find
- **Code** (C/C++/asm/scripts) with **tests** where applicable.  
- **Reproducible evidence:** `evidence/<Phase>/<Block>/<pbrXX>/` → logs, screenshots, hashsets, versions.  
- **Documentation (PAD):** method, risks, limits, and a clear **how-to-reproduce**.  
- **Before/after tables** for evasion/telemetry (from Phase 4 onward).

---

## 6) Quick verification (≈3 minutes)
1. Open `Plan_TryOfCheckDogs.md` and `Syllabus_Summary.md` (scope & timeline).  
2. Enter a phase (e.g., `Phase2_*`) and locate a **PBR** with its **PAD**.  
3. Check **evidence/** (logs, screenshots, hashes) and **tests** (when present).  
4. See `docs/encrypted-missions.md` for the **Encrypted Missions protocol**.  
5. Optional: `docs/progression.md` for status and metrics.

---

## 7) Ethics & scope
- **Isolated lab only**, **benign payloads**, **no** third-party systems.  
- In Phases 4–5, techniques are measured with a **Blue** dashboard (Sysmon/ETW, YARA/Sigma, KQL).  
- The repo **does not** ship operational malware; all content is **educational** and reversible.

---

## 8) Key links
- **Master plan:** `Plan_TryOfCheckDogs.md`  
- **Syllabus summary:** `Syllabus_Summary.md`  
- **Encrypted Missions guide:** `docs/encrypted-missions.md`  
- **Progress & metrics:** `docs/progression.md`  
- **OPSEC/Legal:** `docs/opsec-legal.md`

> If any link isn’t live yet, it’s planned under `docs/` and will be populated as the path advances.

---

## 9) Contact
For a guided 15–20 min walkthrough of the repo and evidence, open an issue tagged **demo-request** or use the contact channel in the profile.
