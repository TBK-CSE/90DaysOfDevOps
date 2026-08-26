# Day 25 – Git Reset vs Revert & Branching Strategies

## Task
Learning how to **undo mistakes** safely — one of Git's most important skills. Also exploring **branching strategies** used by real engineering teams to manage code at scale.

---

## Task 1: Git Reset — Hands-On

Made 3 commits (A, B, C) and tested all three reset modes.

<img width="837" height="75" alt="image" src="https://github.com/user-attachments/assets/cf82d446-0c34-489c-b7ce-778039ae8361" />
<img width="759" height="75" alt="image" src="https://github.com/user-attachments/assets/9abe85df-e12b-464c-a07b-c5d4c67607f9" />
<img width="700" height="223" alt="image" src="https://github.com/user-attachments/assets/b2c8a017-c774-445e-babc-d1f62b85cab3" />
<img width="841" height="125" alt="image" src="https://github.com/user-attachments/assets/3e19d5bf-7a7f-4f33-867c-e061daa06711" />
<img width="814" height="110" alt="image" src="https://github.com/user-attachments/assets/36c31507-50d6-4f49-a7a3-ceaed595458a" />
<img width="693" height="273" alt="image" src="https://github.com/user-attachments/assets/97a4a36e-b74d-40db-8529-07cffd8b721b" />

**`git reset --soft HEAD~1`**
Commit ID moved back one step, but changes stayed exactly as they were — still staged, ready to commit again.

**`git reset --mixed HEAD~1`**
Commit ID moved back one step, changes still present locally — but **unstaged** this time.

**Difference between `--soft` and `--mixed`:** with `--mixed`, changes land back in the working directory as unstaged; with `--soft`, changes stay staged (as if `git add .` was already run).
<img width="1011" height="151" alt="image" src="https://github.com/user-attachments/assets/1591e8d0-553e-433e-a1aa-49edd849cfb3" />
<img width="824" height="93" alt="image" src="https://github.com/user-attachments/assets/3779c9fc-8812-4beb-8963-2b8cdadde3ad" />
<img width="731" height="163" alt="image" src="https://github.com/user-attachments/assets/e2cddc22-c77b-4b06-8a81-d4992a6d36b3" />

**`git reset --hard HEAD~1`**
Both the commit ID *and* the local changes were removed entirely.

**Summary — `--soft` vs `--mixed` vs `--hard`:**
- **`--soft`** → removes the commit, changes stay staged
- **`--mixed`** → removes the commit, changes move to unstaged (still in working dir)
- **`--hard`** → removes the commit *and* all local changes — fully destructive

**Which is destructive?** `--hard` — it's the only one that discards actual file changes, not just commit history.

**Should you use `git reset` on already-pushed commits?** No — it rewrites history, which breaks things for anyone else who's already pulled those commits.

---

## Task 2: Git Revert — Hands-On

Made 3 commits (X, Y, Z), reverted the middle one (Y).
<img width="713" height="76" alt="image" src="https://github.com/user-attachments/assets/18e64705-eb77-4a85-aaf4-3361832c5cc3" />
<img width="759" height="165" alt="image" src="https://github.com/user-attachments/assets/4152c39c-6dbf-41f4-afc2-a42123b998a4" />


**`git reset` vs `git revert`:**
- `reset` → deletes/rewrites history
- `revert` → adds a *new* commit that undoes the changes, original history stays intact

**Is commit Y still in history after revert?** Yes — `git log` still shows it; a new revert commit is added on top instead of removing it.

**Why is revert safer for shared branches?** It preserves history rather than rewriting it, so it never breaks other people's local copies. Reset should only be used when you're certain no one else depends on the commits being removed.

---

## Task 3: Reset vs Revert — Summary

| | `git reset` | `git revert` |
|---|---|---|
| What it does | Moves HEAD back one (or more) commits | Reverts the changes by creating a new commit |
| Removes commit from history? | Yes | No |
| Safe for shared/pushed branches? | No | Yes |
| When to use | Local, unshared fixes | Fixes on a shared repo |

---

## Task 4: Branching Strategies

### GitFlow
**Flow:**
- `main` → production
- `develop` → active working branch
- `feature/*` → new work
- `release/*` → release preparation
- `hotfix/*` → urgent fixes

**Best for:** large teams, scheduled/structured releases.

### GitHub Flow
**Flow:**
- `main` → always deployable
- `feature branch` → PR → merge

**Best for:** startups, fast/continuous deployment.

### Trunk-Based Development
**Flow:**
- Everyone commits to `main`
- Only short-lived branches

**Best for:** high-speed teams, CI/CD-heavy pipelines.

---

**Which strategy fits which context?**
- **Startup shipping fast** → GitHub Flow
- **Large team, scheduled releases** → GitFlow
- **Modern DevOps / CI-CD heavy org** → Trunk-Based Development
