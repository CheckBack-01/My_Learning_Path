
# Guide — Recruiter Overview (TOCD / My_Learning_Path)

**What this is**  
Public repository for **TOCD — Try Of Check Dogs**, a self-directed path in **Reverse Engineering** and **Malware Development** focused on **evasion, persistence, and C2**. All work is done **exclusively in lab VMs** with professional-grade documentation.

**Who should read this**  
Recruiters and hiring managers who need a fast, high-signal overview of the repo’s scope, organization, metrics, and evidence—without browsing the entire tree.

---

## 1) 30-second summary
- Multi-year plan using **PBR** (reproducible labs) + **PAD** (Practical Aptitude Drill, multi-tech mission).
- Realistic progression: **F1 Fundamentals** → **F2 Reversing/Loaders** → **F3 Internals & Exploits** → **F4 Evasion/Persistence/C2** → **F5 Kernel/UEFI**.
- Every block ships **code + evidence + documentation** that’s independently reproducible.
- **Ethics/OPSEC:** lab-only, benign payloads, no testing against third-party systems.

---

## 2) How the repo is organized (top → down)
**Phase → Block → Stack → PBR / PAD**

- **Phase (F1–F5):** macro-objective (e.g., F1 fundamentals, F2 reversing, F3 userland exploitation, F4 evasion/C2, F5 kernel/UEFI).  
- **Block (B1, B2, …):** a concrete topic within a phase (e.g., “PE & in-memory loaders”).  
- **Stack:** a small, sequential topic/tool sequence inside a block.  
- **PBR — Proof-of-Bounty-Readiness:** a **reproducible lab** with clear objectives, datasets/tests, and evidence.  
- **PAD — Practical Aptitude Drill:** a **multi-tech mission per block** that **combines several tactics in one exercise** (e.g., analysis + loader + injection). It’s designed to **prove applied mastery**, not just document. Includes a **short debrief** (results, artifacts, limits, how to reproduce).

> Typical navigation: `PhaseX_*/B*/` → `labs/` (code/PoCs) · `pad/` (aptitude missions) · `evidence/` (artifacts) · `docs/` (reports, protocols).

**Suggested folder layout**

---

## 3) Glossary (short, high-signal)
- **PBR:** reproducible lab with verifiable steps and outputs (often includes sample data + tests).  
- **PAD:** **integrated, multi-tech mission** per block; validates applied mastery; ships with a brief and a concise **debrief**.  
- **Encrypted Mission:** practice delivered as **GPG-encrypted** instructions; decrypted **only inside the VM**.  
- **Capstone:** integrative exercise that chains multiple techniques with a technical defense.  
- **BackLogs:** weekly short katas to keep skills fresh during low-bandwidth periods (e.g., bug-bounty + university).  
- **Evidence:** logs, screenshots, hashsets, environment versions, and test results.

---

## 4) Recommended reading order (big picture)
1. **F1 — Fundamentals:** Linux/CLI, toolchain, C/ASM, ELF/linking.  
2. **F2 — Applied Analysis:** static/dynamic reversing, basic unpack, **PE & in-memory loaders**, classic injection.  
3. **F3 — Internals & Exploits:** PEB/TEB, regions, **ROP/JOP**, heap (Win/Linux), controlled driver RW (lab).  
4. **F4 — Evasion/Persistence/C2:** anti-analysis, dynamic resolution, **persistence** (Win/Linux/macOS), C2 profiling, **blue validation**.  
5. **F5 — Kernel/UEFI:** LKMs/kprobes, benign Windows driver, **DXE** on OVMF, Secure Boot comparison.

---

## 5) What evidence you’ll find
- **Code** (C/C++/asm/scripts) with **tests** where relevant.  
- **Reproducible artifacts:** `evidence/<Phase>/<Block>/<pbrXX or pad>/` → logs, screenshots, hashsets, environment versions.  
- **PAD debriefs:** concise results, limits, and “how to reproduce”.  
- **Before/after tables** for evasion/telemetry (from F4 onward).

---

## 6) 3-minute verification checklist
1. Open `Plan_TryOfCheckDogs.md` and `Syllabus_Summary.md` for scope and schedule.  
2. Enter a phase (e.g., `Phase2_*`), pick a **PBR** and its **PAD**.  
3. Check `evidence/` for artifacts (logs, screenshots, hashes) and any tests.  
4. Read `docs/encrypted-missions.md` for the **Encrypted Mission Protocol**.  
5. Optional: `docs/progression.md` for status and metrics.

---

## 7) Ethics & scope
- **Isolated lab only**, benign payloads, **no third-party systems**.  
- F4/F5 techniques are measured against a **Blue panel** (Sysmon/ETW, YARA/Sigma, KQL).  
- This repo **does not distribute operational malware**; exercises are **educational and reversible**.

---

## 8) Key links (expected locations)
- **General plan:** `Plan_TryOfCheckDogs.md`  
- **Syllabus summary:** `Syllabus_Summary.md`  
- **Encrypted Missions Guide:** `docs/encrypted-missions.md`  
- **Progress & metrics:** `docs/progression.md`  
- **OPSEC/Legal:** `docs/opsec-legal.md`

> If any link is not yet live, it’s planned in `docs/` and will be populated as the path advances.

---

## 9) Contact
For a guided 15–20 min tour of code and evidence, open an issue with the tag **`demo-request`** or use the contact channel in the profile.
