
# PBR\_0B01\_D14 — FHS Baseline & Evidence Pack

**Block:** 0B01 · Linux CLI & Bash Ecosystem
**Phase:** Phase1\_ENIAC
**Purpose:** Establish a **filesystem (FHS) and environment baseline**, record permissions/umask, validate `/tmp`, 
identify the user’s login shell and the real target of `/bin/sh`, and **package reproducible evidence**.

## What was practiced

* Navigating the **FHS** (L1/L2) and identifying key directories
* **umask 027** and permission verification with `stat`
* Sticky bit and safe writes in **`/tmp`**
* Detecting the **user shell** and the real target of **`/bin/sh`**
* Enumerating **large logs** in `/var/log`
* Run log, **manifest**, and **SHA256 checksums**
* Packaging a **tar.gz** with all evidence

## Repo location

This README lives at:
`TryOfCheckDogs/Phases/Phase1_Eniac/Blocks_Evidence/0B01_Linux_CLI_Bash_Ecosystem/PBRs/PBR_FHS_2025-08-27/`
Script: [`pbr_d14_run.sh`](./pbr_d14_run.sh)

## One-command run

```bash
mkdir -p ~/lab && cd ~/lab
cat > pbr_d14_run.sh << 'EOF'
#!/usr/bin/env bash
set -Eeuo pipefail
umask 027
export LC_ALL=C

STAMP="$(date +%F)"
ROOT="${HOME}/lab/D14_${STAMP}"
EVID="${ROOT}/evid"
WORK="${ROOT}/work"

mkdir -p "${EVID}" "${WORK}"

# Log to file and screen
exec > >(tee -a "${EVID}/run.log") 2>&1
echo "[*] D14 start: $(date -Is)"

# 1) Host fingerprint
{ date -Is; uname -a; id; printf 'umask '; umask; } >| "${EVID}/host.txt"
hostnamectl 2>/dev/null >> "${EVID}/host.txt" || true

# 2) FHS L1/L2 and key dirs
( tree -L 1 -d / 2>/dev/null || find / -maxdepth 1 -type d | sort ) >| "${EVID}/fhs_tree_L1.txt"
( tree -L 2 -d / 2>/dev/null || find / -maxdepth 2 -type d | sort ) >| "${EVID}/fhs_tree_L2.txt"
grep -E '^/(bin|sbin|etc|var|lib(32|64)?|home|usr|tmp|run|proc|sys|dev)$' "${EVID}/fhs_tree_L1.txt" >| "${EVID}/fhs_keys.txt" || true

# 3) umask and perms
mkdir -p "${WORK}/demo"/{dirA,dirB}
touch "${WORK}/demo/archivo1.txt"
stat -c '%a %A %U:%G %n' "${WORK}/demo" "${WORK}/demo/archivo1.txt" >| "${EVID}/perms_umask027.txt"

# 4) /tmp sticky and write test
stat -c '%a %A %U:%G %n' /tmp >| "${EVID}/tmp_mode.txt"
touch "/tmp/d14_test_$$"
ls -l "/tmp/d14_test_$$" >| "${EVID}/tmp_touch.txt" || true

# 5) Large logs
find /var/log -type f -size +1M -printf '%10s %p\n' 2>/dev/null \
  | sort -nr | head -n 20 >| "${EVID}/varlogs_big.txt"

# 6) Shell and /bin/sh
getent passwd "$USER" | cut -d: -f7 >| "${EVID}/user_shell.txt"
readlink -f /bin/sh >| "${EVID}/sh_target.txt"

# 7) FHS checklist
for p in /bin /sbin /etc /var /usr /lib /home /tmp /run /proc /sys /dev; do
  if [ -e "$p" ]; then echo "OK: $p"; else echo "MISSING: $p"; fi
done >| "${EVID}/fhs_checklist.txt"

# 8) Manifest and checksums
{
  echo "generated: $(date -Is)"
  echo "mission_id: D14_FHS_BASELINE"
  echo "tool_versions: $(uname -sr)"
} >| "${EVID}/manifest.txt"

sha256sum "${EVID}"/* >| "${EVID}/checksums.txt"

# 9) PBR package
tar -czf "${ROOT}/pbr_d14_$(date +%Y%m%d%H%M%S).tar.gz" -C "${ROOT}" evid
echo "[*] D14 done: ${EVID}"
EOF
chmod +x pbr_d14_run.sh
./pbr_d14_run.sh
```

## Minimum deliverables (`evid/`)

`run.log`, `host.txt`, `fhs_tree_L1.txt`, `fhs_tree_L2.txt`, `fhs_keys.txt`,
`perms_umask027.txt`, `tmp_mode.txt`, `tmp_touch.txt`, `varlogs_big.txt`,
`user_shell.txt`, `sh_target.txt`, `fhs_checklist.txt`, `manifest.txt`, `checksums.txt`,
and the `pbr_d14_*.tar.gz` package.

## Quick verification

```bash
cd ~/lab/D14_YYYY-MM-DD/evid
sha256sum -c checksums.txt
```

