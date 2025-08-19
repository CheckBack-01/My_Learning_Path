
# OPSEC & Legal — Policy and Playbook (TOCD)

**Owner:** Denis Pérez • **Scope:** Entire TOCD repo (labs, docs, evidence, encrypted missions)
**Status:** v1.0 • **Last updated:** 2025-08-19

> **TL;DR**
>
> * **Lab-only.** VMs, benign payloads, snapshots, outbound-only NAT.
> * **Authorized programs only** (Bug Bounty, CTFs, or explicit lab consent).
> * Every block closes with **PBR + PAD** and **reproducible evidence**—without leaking secrets or third-party data.
> * **Encrypted Missions** deliver instructions only via GPG; nothing sensitive in plain text.
> * No operational malware, no real-world targeting, no persistence outside the lab.

---

## 1) Purpose & Scope

Define operational and legal rules for all **Reverse Engineering / Malware Development** work under **TOCD**, ensuring safety, legality, and reproducibility.

* Applies to: source code, scripts, binaries, evidence, documentation, and **Encrypted Missions**.
* Objective: **learn and demonstrate** techniques **in lab only**—**not** to run real campaigns.

---

## 2) Non-Negotiables

1. **Legality & consent:** only on assets you own or with **explicit authorization**.
2. **Isolation:** dedicated VMs with **no** routes to third-party networks or data.
3. **Benign payloads:** harmless, templated, reversible; **rollback guaranteed**.
4. **Reproducibility:** scripts, pinned versions, hashes, and environment notes for every run.
5. **Least privilege:** restrict access, secrets, and artifacts to the minimum necessary.

---

## 3) Allowed Technical Scope (Lab-Only)

* **Dedicated VMs** (Win/Linux/macOS) with **snapshots** per PBR/PAD.
* **Network:** outbound NAT; **no** exposed inbound ports.
* **Workloads:** didactic binaries; **lab** vulnerable drivers only.
* **Tooling:** debuggers, disassemblers, ETW/Sysmon, YARA/Sigma, KQL, etc.
* **Prohibited:** testing on third-party assets, real phishing, or handling real user data.

---

## 4) Engagement Rules (Bug Bounty / CTF)

* Only **authorized programs** and **in-scope windows** (re-check policy every time).
* **No PII exfiltration**; use **synthetic data**.
* Keep tests **minimally invasive**; stop at signs of instability.
* **Responsible Disclosure:**

  * Report with controlled, reproducible proofs.
  * **Never** publish sensitive data or active keys.
  * Follow the program’s disclosure timelines.

---

## 5) Data Classification & Handling

**Levels**

* **Public:** docs, neutral code, diagrams.
* **Internal:** lab evidence (logs, screenshots) **without secrets**.
* **Secret:** dummy creds, GPG keys, lab tokens → **do not** commit.

**Rules**

* Do not commit `secrets.*`, `*.key`, `*.pem`, `*.pfx`, `*.kdbx`, or dumps with tokens.
* Store evidence hashes in `SHA256SUMS.txt`; environment versions in `ENVINFO.md`.

---

## 6) Secret Management

* Local `.env` plus a `dotenv.example` with **no real values**.
* Use GPG for **Encrypted Missions** and any sensitive transport.
* Rotate lab keys/passwords every **90 days**.
* **Never** share secrets via issues/PRs.

---

## 7) Reproducible Builds & Metadata Hygiene

* Pin versions and set **`SOURCE_DATE_EPOCH`**.
* **Strip** symbols in public binaries; keep symbols **lab-only**.
* Normalize timestamps/timezones in evidence and reports.
* Avoid user paths embedded in public artifacts.

---

## 8) Safe Publishing Checklist (Pre-Push)

* [ ] No secrets or PII present.
* [ ] Evidence sanitized (internal hostnames/IPs obfuscated).
* [ ] Demo binaries **signed** or **stripped**, as appropriate.
* [ ] `README`/`PAD` include **how to reproduce** in lab.
* [ ] Educational/license notice included.

---

## 9) Encrypted Mission Protocol (GPG)

* **Location:** `missions/encrypted/`
* **Format:** **ASCII-armored GPG** blocks only in public repos; never plain-text instructions.
* **VM Flow:**

  1. Save the block as `mission.gpg`.
  2. Run `gpg --decrypt mission.gpg` (lab password).
  3. Execute in the VM; store evidence under `evidence/...`.

> **Forbidden:** committing plain-text instructions or mission passwords.

---

## 10) Evidence & Chain of Custody

Recommended structure per PBR/PAD:

```
evidence/F#/B#/pbrXX/
  ├─ logs/
  ├─ screenshots/
  ├─ artifacts/          # benign lab dumps/binaries
  ├─ ENVINFO.md          # OS, toolchain, hashes, seeds
  └─ SHA256SUMS.txt      # artifact hashset
```

* Evidence must be **reproducible**, minimal, and secret-free.
* Record exact tool versions and hashes.

---

## 11) Networking, Isolation & Snapshots

* **Outbound NAT only**; no port forwarding.
* **Snapshots:** before/after each PBR/PAD; verify restore.
* **USB blocked** to VMs except approved **lab** hardware (F4-12D..12F).
* **DNS:** prefer internal resolver or reputable public DNS.

---

## 12) Account & Access Security

* Enforce 2FA on GitHub and lab accounts.
* Use tokens with **minimal scopes** and expirations.
* Private repos: least-privilege membership and change tracking.

---

## 13) Quick Templates

**13.1 — Lab Consent (template)**

```text
Lab Consent — TOCD
Environment: personal host with dedicated VM(s), NAT only, no third-party access.
Purpose: educational training; no testing on non-consenting systems.
Scope: didactic binaries/artifacts, benign payloads, guaranteed rollback.
Signed: ____________________   Date: __________
```

**13.2 — OPSEC Header for PBR/PAD**

```markdown
> OPSEC/Legal: lab-only · NAT · benign payloads · no third-party data · snapshot OK
> Reproducible via: `make lab-setup && make run`
> Evidence: `evidence/Fx/Bx/pbrYY/` (hashes + ENVINFO.md)
```

**13.3 — Evidence Manifest**

```text
Manifest
- Run ID: <UTC timestamp + seed>
- Host/VM: <OS build, kernel, locale>
- Tools: <versions pinned>
- Files + SHA256: see SHA256SUMS.txt
- Notes: deviations, mitigations, risks
```

**13.4 — GPG Mini-Cheatsheet**

```bash
# Create lab keypair
gpg --quick-generate-key "TOCD Lab <lab@example>" ed25519 sign 0
gpg --quick-add-key "<fingerprint>" cv25519 encrypt 0
# Encrypt (ASCII)
gpg --armor --encrypt --recipient "TOCD Lab" mission.txt > mission.gpg
# Decrypt
gpg --decrypt mission.gpg
```

---

## 14) Incident Response (What to do if…)

* **Secret leaked:** revoke/rotate creds, remove artifact, log incident under `docs/incidents/`.
* **Instability outside lab:** stop, document, restore snapshot, root-cause.
* **Bug Bounty report with sensitive data:** contact program, sanitize, **do not publish**.
* **Legal/ethical risk:** pause, review policy, **do not proceed** until cleared.

---

## 15) Legal & Ethical Boundaries (Red Lines)

* No testing on third-party infrastructure **without permission**.
* No DoS, ransomware, cryptojacking, or persistence outside lab.
* No distribution of operational malware.
* No real personal data; use synthetic datasets only.

---

## 16) Licensing & Educational Use

* This repository and artifacts are for **educational purposes**.
* Code and PoCs are designed to function **in lab environments only**.
* Add a visible notice in `README.md` and in each PAD/PBR.

---

## 17) Auditability & Traceability

* Descriptive commits; issues/milestones aligned with **KPIs**.
* Record hashes and versions per PBR/PAD.
* Version YARA/Sigma/KQL rule changes under `rules/`.

---

## 18) Related Documents

* `Plan.md` — Overall plan and calendar.
* `docs/Public_Schedule.md` — Public quarterly schedule.
* `docs/progression.md` — PBR/PAD progress.
* `docs/encrypted-missions.md` — Encrypted Mission Protocol.

---

### Appendix A — Suggested Control Files

**.gitignore (excerpt)**

```
# Secrets / keys
*.pem
*.key
*.pfx
*.kdbx
.env
.env.*
# Local artifacts
*.dmp
*.core
*.pcap
*.mem
# Evidence big files (keep hashes only)
evidence/**/artifacts/*.bin
evidence/**/artifacts/*.img
```

**.gitattributes (deterministic timestamps)**

```
* text=auto
*.sh eol=lf
*.md eol=lf
```

---

**Compliance**
By contributing to or using this repo, you agree to follow this **OPSEC & Legal Playbook**. Any deviation must be documented and approved **before** execution.
