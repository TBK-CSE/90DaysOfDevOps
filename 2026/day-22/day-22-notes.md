# Day 22 – Introduction to Git: Your First Repository

## Task
The beginning of the Git journey. Git is the backbone of modern DevOps — every tool, pipeline, and workflow revolves around version control. Getting comfortable with the basics by doing.

**Covers:**
- What Git is and why it matters
- Setting up the first Git repository from scratch
- Building a living document of Git commands

---

## Task 1: Install and Configure Git
1. Verify Git is installed
2. Set up Git identity — name and email
3. Verify the configuration

## Task 2: Create the Git Project
1. Create folder `devops-git-practice`
2. Initialize it as a Git repository
3. Check status — read and understand what Git reports
4. Explore the hidden `.git/` directory

## Task 3: Git Commands Reference
1. Create `git-commands.md` inside the repo
2. Add commands used so far, organized by category:
   - Setup & Config
   - Basic Workflow
   - Viewing Changes
3. For each: what it does (1 line) + an example

## Task 4: Stage and Commit
1. Stage the file
2. Check what's staged
3. Commit with a meaningful message
4. View commit history

## Task 5: Build History
1. Edit `git-commands.md` — add more commands as discovered
2. Check what changed since the last commit
3. Stage and commit again with a different, descriptive message
4. Repeat at least 3 times to build multiple commits
5. View the full history in compact format

---

## Task 6: Understanding the Git Workflow

**1. `git add` vs `git commit`**
- `git add` → moves changes to the staging area
- `git commit` → saves the staged changes permanently to history

**2. What does the staging area do?**
It's a buffer where changes are prepared before committing (`git add .`). Git doesn't commit directly because staging lets you review and choose exactly what goes into a commit — instead of committing every change in the working directory blindly.

**3. What does `git log` show?**
Commit history — messages, author, timestamps (`git log`).

**4. What is the `.git/` folder?**
Contains all repository data — history, config, objects, refs. If deleted, the repo's history is lost (it's effectively the repo's metadata/database).

**5. Working directory vs staging area vs repository**
- **Working directory** → current files as they exist on disk
- **Staging area** → changes marked ready to commit (`git add .`)
- **Repository** → the saved, committed history

---

## Screenshots

**`git log --oneline` output:**

<img width="1078" height="997" alt="image" src="https://github.com/user-attachments/assets/77211f2f-d0ee-4ca3-be7e-721f2b768204" />


**Exploring the `.git/` folder contents:**
<img width="833" height="380" alt="image" src="https://github.com/user-attachments/assets/dccd23a0-6c76-4212-af65-c51162395440" />

