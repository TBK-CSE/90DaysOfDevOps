# Day 09 – Linux User & Group Management Challenge

## Task
Practice user and group management through hands-on challenges:
- Create users and set passwords
- Create groups and assign users
- Set up shared directories with group permissions

---

## Task 1: Create Users
Create three users with home directories and passwords: `tokyo`, `berlin`, `professor`.
**Verify:** check `/etc/passwd` and `/home/`.

**Commands used:**
```
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m professor
```
`-m` creates the home directory (e.g. `/home/tokyo`) for the mentioned user.
<img width="1089" height="859" alt="image" src="https://github.com/user-attachments/assets/a228cd8a-0beb-47d9-b69a-0ed322e77ca5" />

**Setting passwords:**

<img width="605" height="150" alt="image" src="https://github.com/user-attachments/assets/43a0f7de-f8ef-4952-afec-d437fe89116e" />


**Verification:**
```
cat /etc/passwd && ls /home
```

---

## Task 2: Create Groups
Create two groups: `developers`, `admins`.
**Verify:** check `/etc/group`.

**Commands used:**
```
sudo groupadd developers
sudo groupadd admins
```

**Verification:**
```
cat /etc/group | grep "developers"
```

---

## Task 3: Assign Users to Groups
*(~15 min)*

Assignments:
- `tokyo` → developers
- `berlin` → developers + admins (both groups)
- `professor` → admins

**Commands used:**
<img width="858" height="76" alt="image" src="https://github.com/user-attachments/assets/29f4eb9b-ce6c-42dc-b4f5-767a5f6d5a3e" />
<img width="285" height="35" alt="image" src="https://github.com/user-attachments/assets/297cc68d-42a7-422d-abc5-3c4abfab9972" />



Verified using the appropriate group-membership check command.

---

## Task 4: Shared Directory

- Create `/opt/dev-project`
- Set group owner to `developers`
- Set permissions to `775` (`rwxrwxr-x`)
- Test by creating files as `tokyo` and `berlin`

**Commands used:**

<img width="790" height="466" alt="image" src="https://github.com/user-attachments/assets/2b5219bf-1409-4e8a-b39a-8c344d63db73" />


---

## Task 5: Team Workspace
*(~20 min)*

- Create user `nairobi` with home directory
- Create group `project-team`
- Add `nairobi` and `tokyo` to `project-team`
- Create `/opt/team-workspace`
- Set group to `project-team`, permissions to `775`
- Test by creating a file as `nairobi`

**Commands used:**
<img width="704" height="202" alt="image" src="https://github.com/user-attachments/assets/ed059984-ebc9-4734-b91a-d42c4817397d" />


---

## Summary

**Users & Groups Created**
- Users: `tokyo`, `berlin`, `professor`, `nairobi`
- Groups: `developers`, `admins`, `project-team`

**Group Assignments**
- `tokyo` → developers, project-team
- `berlin` → developers, admins
- `professor` → admins
- `nairobi` → project-team

**Directories Created**
- `/opt/dev-project` → developers group, `775`
- `/opt/team-workspace` → project-team group, `775`

**Commands Used**
`useradd`, `passwd`, `groupadd`, `usermod`, `chgrp`, `chmod`

**What I Learned**
- How to manage users and groups
- How permissions control access
- How shared directories work in real systems
