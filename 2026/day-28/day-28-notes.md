# Day 28 – Revision Day: Everything from Day 1 to Day 27

## Task
Consolidate everything covered across the first 27 days before moving forward.

---

## What's Been Covered So Far

| Days | Topic | Key Concepts |
|------|-------|-------------|
| 1 | DevOps & Cloud Intro | What is DevOps, SDLC, Cloud basics |
| 2–7 | Linux Fundamentals | Architecture, commands, processes, systemd, file system hierarchy, troubleshooting, text files |
| 8 | Cloud Server Setup | Docker, Nginx, web deployment |
| 9–11 | Users, Permissions & Ownership | User/group management, file permissions, chown/chgrp |
| 12 | Revision Day 1 | Days 1–11 recap |
| 13 | Volume Management | LVM — physical volumes, volume groups, logical volumes |
| 14–15 | Networking | Fundamentals, DNS, IP, subnets, ports, hands-on checks |
| 16–18 | Shell Scripting | Basics, loops, arguments, error handling, functions |
| 19–20 | Shell Scripting Projects | Log rotation, backup, crontab, log analyzer |
| 21 | Shell Scripting Cheat Sheet | Personal reference guide |
| 22–25 | Git & GitHub | Init, branching, merge, rebase, stash, cherry pick, reset, revert, branching strategies |
| 26 | GitHub CLI | Managing GitHub from the terminal |
| 27 | GitHub Profile | Profile README, repo organization, developer branding |

---

## Skills Checklist

**Linux**
- [x] Navigate the file system, create/move/delete files and directories
- [x] Manage processes — list, kill, background/foreground
- [x] Work with systemd — start, stop, enable, check status of services
- [x] Read and edit text files using vi/vim or nano
- [x] Troubleshoot CPU, memory, and disk issues using top, free, df, du
- [x] Explain the Linux file system hierarchy (/, /etc, /var, /home, /tmp, etc.)
- [x] Create users and groups, manage passwords
- [x] Set file permissions using chmod (numeric and symbolic)
- [x] Change file ownership with chown and chgrp
- [x] Create and manage LVM volumes
- [x] Check network connectivity — ping, curl, netstat, ss, dig, nslookup
- [x] Explain DNS resolution, IP addressing, subnets, and common ports

**Shell Scripting**
- [x] Write a script with variables, arguments, and user input
- [x] Use if/elif/else and case statements
- [x] Write for, while, and until loops
- [x] Define and call functions with arguments and return values
- [x] Use grep, awk, sed, sort, uniq for text processing
- [x] Handle errors with set -e, set -u, set -o pipefail, trap
- [x] Schedule scripts with crontab

**Git & GitHub**
- [x] Initialize a repo, stage, commit, and view history
- [x] Create and switch branches
- [x] Push to and pull from GitHub
- [x] Explain clone vs fork
- [x] Merge branches — understand fast-forward vs merge commit
- [x] Rebase a branch and explain when to use it vs merge
- [x] Use git stash and git stash pop
- [x] Cherry-pick a commit from another branch
- [x] Explain squash merge vs regular merge
- [x] Use git reset (soft, mixed, hard) and git revert
- [x] Explain GitFlow, GitHub Flow, and Trunk-Based Development
- [x] Use GitHub CLI to create repos, PRs, and issues

---

## Gap-Filling: LVM Revisited

Revisited the Day 13 notes to solidify LVM steps:

```bash
lsblk                                          # list all block devices
pvcreate /dev/your_storage_name                # create a physical volume on the new disk
pvs                                             # check physical volumes
vgcreate storage-vg /dev/storage                # create a volume group
vgs                                             # list volume groups
lvcreate -L 2G -n app-data storage-vg           # create a 2G logical volume "app-data" under storage-vg
mkfs.ext4 /dev/devops-vg/app-data               # format it with a filesystem
mkdir /tmp/data                                 # create the mount point
mount /dev/devops-vg/app-data /tmp/data         # mount it — /tmp/data now has 2G of storage
```

---

## Gap-Filling: Branching Strategies

**GitFlow** — `develop`, `feature`, `release`, `hotfix` branches.
**GitHub Flow** — simple: single `main` branch + feature branches.
**Trunk-Based Development** — everyone commits to `main`, short-lived branches only.

**GitFlow**
```
main    → production
develop → active working branch
feature → new work
release → release prep
hotfix  → urgent fixes
```
**Use for:** big teams, scheduled releases.

**GitHub Flow**
```
main            → always deployable
feature branch  → PR → merge
```
**Use for:** startups, fast/continuous deployment.

**Trunk-Based**
```
main → everyone commits directly
short-lived branches only
```
**Use for:** high-speed teams, CI/CD-heavy orgs.

**Which fits which context:**
- Startup → GitHub Flow
- Large team → GitFlow
- Modern DevOps org → Trunk-Based

---

## Quick-Fire Questions (answered from memory, then verified)

**1. What does `chmod 755 script.sh` do?**
Sets permissions: owner → read/write/execute, group → read/execute, others → read/execute.

**2. Difference between a process and a service?**
A **process** is any running program. A **service** is a long-running background process managed by the system (via systemd).

**3. How do you find which process is using port 8080?**
`lsof -i :8080` or `ss -tulpn | grep 8080`

**4. What does `set -euo pipefail` do?**
- `-e` → exit immediately on any command failure
- `-u` → exit if an unset variable is used
- `-o pipefail` → fail the whole pipeline if any command within it fails (not just the last one)

**5. Difference between `git reset --hard` and `git revert`?**
`reset --hard` removes the commit from history *and* discards local changes entirely. `revert` undoes the changes by creating a new commit, keeping the full history intact.

**6. Branching strategy for a team of 5 shipping weekly?**
GitHub Flow.

**7. What does `git stash` do, and when to use it?**
Temporarily shelves uncommitted changes. Useful when switching branches mid-work without wanting those changes to carry over or get committed prematurely.

**8. How do you schedule a script to run daily at 3 AM?**
`0 3 * * * /path/to/script.sh`

**9. Difference between `git fetch` and `git pull`?**
`fetch` downloads changes only. `pull` downloads *and* merges them (`fetch` + `merge`).

**10. What is LVM, and why use it over regular partitions?**
LVM (Logical Volume Manager) gives flexibility to resize storage dynamically — volumes can be extended on the fly as usage grows, something fixed partitions can't do easily.

---

## Teach-It-Back: File Permissions

**What is a file permission?**
Controls who can read, write, or execute a file. In Linux, permissions can be viewed and modified directly.

**Breaking down `chmod 755 script.sh`:**
`chmod` = "change mode." The three digits represent owner, group, and others respectively.

Each digit is a sum of:
- `4` → read
- `2` → write
- `1` → execute

So `7` = 4+2+1 = read+write+execute, `5` = 4+1 = read+execute.

Example combos: `6` = 4+2 = read/write, `3` = 1+2 = write/execute.

The target is a file name at the end — but the same `chmod` syntax works identically on folders too.
