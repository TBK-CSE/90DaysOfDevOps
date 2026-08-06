# Day 11 – File Ownership Challenge (chown & chgrp)

## Task
Master file and directory ownership in Linux.
- Understand file ownership (user and group)
- Change file owner using `chown`
- Change file group using `chgrp`
- Apply ownership changes recursively

---

## Task 1: Understanding Ownership

- Run `ls -l` in home directory
- Identify the owner and group columns
- Check who owns your files
- Format: `-rw-r--r-- 1 owner group size date filename`

**Owner vs Group:**
- **Owner** → who controls the file
- **Group** → shared access for a pool of users

*[screenshot: ls -l ownership output]*

---

## Task 2: Basic chown Operations

- Create `devops-file.txt`
- Check current owner: `ls -l devops-file.txt`
- Change owner to `tokyo` (create user if needed)
- Change owner to `berlin`
- Verify the changes

*[screenshot: chown operations]*

---

## Task 3: Basic chgrp Operations

- Create `team-notes.txt`
- Check current group: `ls -l team-notes.txt`
- Create group: `sudo groupadd heist-team`
- Change file group to `heist-team`
- Verify the change

*[screenshot: chgrp operations]*

---

## Task 4: Combined Owner & Group Change

`chown` can change both owner and group in one command: `chown professor:heist-team file_name`

- Create `project-config.yaml`, change owner to `professor` and group to `heist-team` (single command)
- Create directory `app-logs/`, change owner to `berlin` and group to `heist-team`

*[screenshot: combined chown operations]*

---

## Task 5: Recursive Ownership

**Setup:**
```
mkdir -p heist-project/vault
mkdir -p heist-project/plans
touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
sudo groupadd planners
```

- Change ownership of the entire `heist-project/` directory:
  - Owner: `professor`
  - Group: `planners`
  - Use recursive flag (`-R`)
- Verify: `ls -lR heist-project/`

*[screenshot: recursive ownership change]*

---

## Task 6: Practice Challenge

- Create users: `tokyo`, `berlin`, `nairobi` (if not already created)
- Create groups: `vault-team`, `tech-team`
- Create directory `bank-heist/` with 3 files:
  ```
  touch bank-heist/access-codes.txt
  touch bank-heist/blueprints.pdf
  touch bank-heist/escape-plan.txt
  ```
- Set ownership:
  - `access-codes.txt` → owner: `tokyo`, group: `vault-team`
  - `blueprints.pdf` → owner: `berlin`, group: `tech-team`
  - `escape-plan.txt` → owner: `nairobi`, group: `vault-team`
- Verify: `ls -l bank-heist/`

*[screenshot: final ownership verification]*

---

## Summary

**Files & Directories Created**
`devops-file.txt`, `team-notes.txt`, `project-config.yaml`, `heist-project/`, `bank-heist/`

**Ownership Changes**
- `devops-file.txt` → tokyo → berlin
- `team-notes.txt` → group changed to heist-team
- `project-config.yaml` → professor:heist-team
- `heist-project` → professor:planners (recursive)

**Commands Used**
`chown`, `chgrp`, `ls`, `mkdir`, `touch`

**What I Learned**
- Difference between owner and group
- How to change ownership using `chown`
- How recursive ownership works
