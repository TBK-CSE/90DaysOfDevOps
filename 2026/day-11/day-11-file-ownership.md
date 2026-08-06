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

<img width="676" height="203" alt="image" src="https://github.com/user-attachments/assets/0bd9b550-c7a1-430a-a324-9dac134be964" />


---

## Task 2: Basic chown Operations

- Create `devops-file.txt`
- Check current owner: `ls -l devops-file.txt`
- Change owner to `tokyo` (create user if needed)
- Change owner to `berlin`
- Verify the changes
<img width="578" height="246" alt="image" src="https://github.com/user-attachments/assets/685b66e1-2f5e-4c07-a3ab-a85547ad2840" />
<img width="584" height="288" alt="image" src="https://github.com/user-attachments/assets/97ef47e2-e5f2-48ee-a1b8-50a2985434ab" />
<img width="558" height="78" alt="image" src="https://github.com/user-attachments/assets/8cd8c513-f4c6-4bc6-99f8-35528d89d418" />



---

## Task 3: Basic chgrp Operations

- Create `team-notes.txt`
- Check current group: `ls -l team-notes.txt`
- Create group: `sudo groupadd heist-team`
- Change file group to `heist-team`
- Verify the change

<img width="531" height="92" alt="image" src="https://github.com/user-attachments/assets/e3dcc055-94b6-4f68-9761-d0edbd2ea3f6" />
<img width="1186" height="127" alt="image" src="https://github.com/user-attachments/assets/3501e2e8-a905-4ffe-99f6-4ee2362f1d4b" />


---

## Task 4: Combined Owner & Group Change

`chown` can change both owner and group in one command: `chown professor:heist-team file_name`

- Create `project-config.yaml`, change owner to `professor` and group to `heist-team` (single command)
- Create directory `app-logs/`, change owner to `berlin` and group to `heist-team`
<img width="727" height="368" alt="image" src="https://github.com/user-attachments/assets/27005c45-5db1-4c69-9469-a273dd4e85a0" />c
<img width="607" height="110" alt="image" src="https://github.com/user-attachments/assets/3ecb379b-275c-497d-8e9d-8b9c8c760f8b" />




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
<img width="1650" height="529" alt="image" src="https://github.com/user-attachments/assets/62b95462-0607-4020-85ef-a40392b28139" />


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
<img width="882" height="755" alt="image" src="https://github.com/user-attachments/assets/6342e980-7c7a-4d10-bae0-610fd0f30c29" />


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
