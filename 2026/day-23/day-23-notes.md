# Day 23 – Git Branching & Remote Concepts

## 1. What is a branch?
A separate line of development that lets you work without affecting the main codebase.

## 2. Why use branches?
To work on features safely, in isolation, without risking or breaking the main branch.

## 3. What is HEAD?
A pointer to the current branch/commit you're currently working on.

## 4. What happens when switching branches?
Files in the working directory change to match the state of the branch being switched to.

## 5. `origin` vs `upstream`
- **origin** → your own repository
- **upstream** → the original repository (the one you forked from)

## 6. `fetch` vs `pull`
- **fetch** → downloads changes from the remote, but doesn't merge them
- **pull** → downloads changes *and* merges them into the current branch (`fetch` + `merge`)

## 7. `clone` vs `fork`
- **clone** → copies a repository locally onto your machine
- **fork** → copies a repository into your own GitHub account

## 8. When to use which?
- **clone** → when you own the repo (or already have access)
- **fork** → when contributing to someone else's repo
