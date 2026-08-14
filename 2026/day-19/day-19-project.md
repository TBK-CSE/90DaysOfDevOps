# Day 19 – Shell Scripting Project: Log Rotation, Backup & Crontab

## Task
Apply everything from Days 16–18 into real-world mini projects.

**Covers:**
- Writing a **log rotation** script
- Writing a **server backup** script
- Scheduling both with **crontab**

---

## Task 1: Log Rotation Script

`log_rotate.sh`:
1. Takes a log directory as an argument (e.g. `/var/log/myapp`)
2. Compresses `.log` files older than 7 days using `gzip`
3. Deletes `.gz` files older than 30 days
4. Prints how many files were compressed and deleted
5. Exits with an error if the directory doesn't exist
<img width="972" height="964" alt="image" src="https://github.com/user-attachments/assets/c1051309-a3bd-4c74-9970-3d36e9d21646" />


---

## Task 2: Server Backup Script

`backup.sh`:
1. Takes a source directory and backup destination as arguments
2. Creates a timestamped `.tar.gz` archive (e.g. `backup-2026-02-08.tar.gz`)
3. Verifies the archive was created successfully
4. Prints archive name and size
5. Deletes backups older than 14 days from the destination
6. Handles errors — exits if source doesn't exist

<img width="524" height="866" alt="image" src="https://github.com/user-attachments/assets/4b9d746e-ace3-43c6-a757-a11fbbd1c397" />


---

## Task 3: Crontab

1. `crontab -l` — check what's currently scheduled
2. Cron syntax:
   ```
   * * * * *  command
   │ │ │ │ │
   │ │ │ │ └── Day of week (0-7)
   │ │ │ └──── Month (1-12)
   │ │ └────── Day of month (1-31)
   │ └──────── Hour (0-23)
   └────────── Minute (0-59)
   ```
3. Cron entries drafted (not applied):

<img width="1141" height="553" alt="image" src="https://github.com/user-attachments/assets/15084f3b-2897-4735-a7fa-5ef72a87750a" />


```bash
# log_rotate.sh — daily at 2 AM
0 2 * * * ./log_rotation.sh /var/log/myapps

# backup.sh — daily at 3 AM
0 3 * * * ./backup.sh /tmp/source-data /tmp/backups

# health_check.sh — every 5 minutes
*/5 * * * * ./health_check.sh
```

> **Note:** minute field set to `0` (not `*`) for the daily jobs — `*` in the minute slot would fire every minute of that hour, not once.

---

## Task 4: Combine — Scheduled Maintenance Script

`maintenance.sh`:
1. Calls the log rotation function
2. Calls the backup function
3. Logs all output to `/var/log/maintenance.log` with timestamps
4. Cron entry to run it daily at 1 AM

<img width="696" height="540" alt="image" src="https://github.com/user-attachments/assets/dfd71512-8984-4a6b-b986-bf34434b276a" />

<img width="1210" height="534" alt="image" src="https://github.com/user-attachments/assets/d9353545-df88-47b8-9886-200eac0329f0" />

---

## Scripts Created
`log_rotate.sh`, `backup.sh`, `maintenance.sh`

## Cron Jobs

```
* * * * *  command
│ │ │ │ │
│ │ │ │ └── Day of week (0-7)
│ │ │ └──── Month (1-12)
│ │ └────── Day of month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

Edited via `crontab -e` (opens in vim editor).

## What I Learned
- Automating real tasks like logs and backups
- Scheduling jobs using cron
- Writing production-like scripts
