# Day 25 – Git Reset vs Revert & Branching Strategies

## Task
Learning how to **undo mistakes** safely — one of Git's most important skills. Also exploring **branching strategies** used by real engineering teams to manage code at scale.

---

## Task 1: Git Reset — Hands-On

Made 3 commits (A, B, C) and tested all three reset modes.

*[screenshot: git reset --soft demo]*

**`git reset --soft HEAD~1`**
Commit ID moved back one step, but changes stayed exactly as they were — still staged, ready to commit again.

**`git reset --mixed HEAD~1`**
Commit ID moved back one step, changes still present locally — but **unstaged** this time.

**Difference between `--soft` and `--mixed`:** with `--mixed`, changes land back in the working directory as unstaged; with `--soft`, changes stay staged (as if `git add .` was already run).

*[screenshot: git reset --hard demo]*

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

*[screenshot: git revert demo]*

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
