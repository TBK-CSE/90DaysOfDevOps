# Day 26 – GitHub CLI: Manage GitHub from Your Terminal

## Task
Switching to the browser to create a PR, check an issue, or manage a repo breaks flow. The **GitHub CLI (`gh`)** lets you do all of that without leaving the terminal — essential for automating workflows, scripting PR reviews, and managing repos at scale.

---

## Task 1: Install and Authenticate

1. Install the GitHub CLI
2. Authenticate with a GitHub account
3. Verify login and check the active account

**Authentication methods `gh` supports:**
- GitHub.com login
- HTTPS
- Browser-based login

---

## Task 2: Working with Repositories

1. Create a new GitHub repo directly from the terminal — public, with a README
2. Clone a repo using `gh` instead of `git clone`
3. View repo details from the terminal
4. List all repositories
5. Open a repo in the browser directly from the terminal
6. Delete the test repo afterward

**Created and cloned a test repo — `test-gh-repo`:**
<img width="1835" height="724" alt="image" src="https://github.com/user-attachments/assets/46ed36a5-d80a-406c-b0cb-9da888ced720" />


---

## Task 3: Issues

1. Create an issue on a repo from the terminal — title, body, and label
2. List all open issues
3. View a specific issue by number
4. Close an issue from the terminal

<img width="1825" height="297" alt="image" src="https://github.com/user-attachments/assets/aeea71fc-ddc1-4b0b-82dd-1679b25b264d" />

**How `gh issue` fits into automation:**
Useful whenever a workflow needs to programmatically create or close issues — e.g. a developer automating issue tracking as part of a script or pipeline.

---

## Task 4: Pull Requests

1. Create a branch, make a change, push it, and create a PR entirely from the terminal
2. List all open PRs on a repo
3. View PR details — status, reviewers, checks
4. Merge the PR from the terminal



**Merge methods `gh pr merge` supports:**
- Squash & merge
- Merge
- Rebase

---
<img width="1435" height="851" alt="image" src="https://github.com/user-attachments/assets/f7eacc06-52f4-46be-b126-7ba2500197f5" />


## Task 5: GitHub Actions & Workflows (Preview)

1. List workflow runs on a public repo using GitHub Actions
2. View the status of a specific workflow run

**How `gh run` / `gh workflow` help in CI/CD:**
- Checking CI/CD status directly from the terminal
- Debugging pipeline failures without switching to the browser
<img width="592" height="75" alt="image" src="https://github.com/user-attachments/assets/73f6de45-0501-4aac-b30b-63cb5ed7aa39" />

---

## Task 6: Useful `gh` Tricks

Explored:
1. `gh api` — raw GitHub API calls from the terminal
2. `gh gist` — create and manage Gists
3. `gh release` — create and manage releases
4. `gh alias` — shortcuts for frequently-used commands
5. `gh search repos` — search GitHub repos from the terminal

**Tried:**
```
gh search repos devops
gh gist create file.txt
```
<img width="1834" height="659" alt="image" src="https://github.com/user-attachments/assets/d27dbab2-0c57-4128-b81e-af790742faf1" />
![Uploading image.png…]()

---


## Summary

**Authentication:** `gh` supports both browser login and token-based authentication.

**Repo Management:** Create, view, list, and delete repos — all from the terminal.

**Issues:** Create, list, view, and close issues via CLI.

**Pull Requests:** Create and merge PRs directly from the terminal.

**Merge Methods:** merge, squash, rebase.

**`gh` in CI/CD:** Useful for automating PRs, checking workflow status, and managing repos without leaving the terminal.
