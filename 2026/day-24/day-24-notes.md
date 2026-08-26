# Day 24 – Git Branching & Working with GitHub

## Task
Now that repo creation, staging, and committing are covered — time for the most powerful concept in Git: **branching**. Branches let you work on features, fixes, and experiments in isolation without breaking main code. Also pushed to GitHub for the first time.

---

## Task 1: Understanding Branches

**Fast-forward merge**
Happens when the target branch has no new commits — Git simply moves the pointer forward, no real "merge" needed.

**Merge commit**
Happens when both branches have new commits and their histories have diverged — Git creates a dedicated merge commit tying both together.

**Conflict handling**
Hit a `CONFLICT` message after editing the same line on two different branches and running `git merge feature-signup`. Resolved the conflicting lines manually and completed the merge.

---

## Task 2: Git Rebase — Hands-On

- Rebasing created a conflict along the way
- After a successful rebase, all commits from `master` appeared in `feature-dashboard`
- **History shape:** merge history is non-linear; rebase history is linear and clean

**Why never rebase commits that have already been pushed and shared?**
Rebase rewrites commit history and changes commit IDs. If those commits are already pushed and others have based work on them:
- their local history diverges from the rewritten one
- this causes conflicts and confusion when they try to pull/push

**Steps to resolve a rebase conflict:**
1. Conflict occurs
2. Fix the conflicting file
3. `git add <file>`
4. `git rebase --continue`

---

## Task 3: Squash Commit vs Merge Commit

- After a squash, many commits collapsed into a single commit in history
- **Difference:** `--squash` produces one single commit for everything; a normal merge preserves the full commit history
- **Trade-off of squashing:** individual commit history is lost — harder to trace who did what and when

---

## Task 4: Git Stash — Hands-On

**`git stash pop` vs `git stash apply`**
- `stash pop` → applies the stash **and removes it** from the stash list
- `stash apply` → applies the stash **but keeps it** in the stash list

**When to use stash in the real world:**
- There's unfinished work in progress
- Need to switch branches urgently
- Don't want to commit incomplete/broken code

---

## Task 5: Cherry Picking

**What does cherry-pick do?**
Applies a specific commit from another branch onto the current branch — instead of merging the whole branch, only the needed change is picked.

**When to use cherry-pick:**
- Need a specific fix (hotfix) without the full feature branch
- Urgent production fix that shouldn't wait for a full merge
