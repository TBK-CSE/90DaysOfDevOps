# Day 07 – Linux File System Hierarchy & Scenario-Based Practice

**Goal:** Understand where things live in Linux, and practice troubleshooting through real-world scenarios.

Split into two sections: **File System Hierarchy** and **Scenario Practice**.

---

## Part 1: File System Hierarchy

### `/` (root)
Contains everything in Linux — the starting point of the filesystem.

```
ls -l /
```
**Observation:** Directories like `bin`, `etc`, `home`. This is the top of the tree — everything else branches off from here.

---

### `/home`
Contains user directories.

```
ls -l /home
```
**Observation:** Individual user folders present. Used to access user files — a system can have multiple users (e.g. `vishal/`, `sonith/`).

---

### `/etc`
Stores configuration files — system configs, service configs, user/account configs.

```
ls -l /etc
```
**Observation:** Files like `hostname` (system info) and `passwd` (user account info). Used to check or edit configs.

---

### `/var/log`
Contains system logs.

```
ls -l /var/log
```
**Observation:** `syslog`, `auth.log`. Used during debugging.

---

### `/tmp`
Temporary files directory.

```
ls -l /tmp
```
**Observation:** Temp files. Used for short-lived, disposable storage.

---

### `/root`
Home directory for the root (admin) user — **not the same** as `/` (root filesystem).
- `/` → the entire system
- `/root` → home folder of the root user

```
ls -l /root
```
**Observation:** Files and configs specific to the root user. Used when working as root or accessing admin-level files.

---

### `/bin`
Essential command binaries — basic commands needed to run the system.

```
ls -l /bin
```
**Observation:** Commands like `ls`, `cp`, `mv`, `cat`. Stores the core commands required for normal system operation.

---

### `/usr/bin`
User-level command binaries (non-critical, non-boot commands).

```
ls -l /usr/bin
```
**Observation:** Commands like `git`, `python`, `curl`. Stores most user-installed or system-installed applications.

---

### `/opt`
Optional or third-party applications.

```
ls -l /opt
```
**Observation:** Folders for custom apps (e.g. `/opt/google/`, `/opt/custom-app`). Used for software outside the default system packages — manual installs or external tools.

---

### Extra Practice

**Find the largest log file in `/var/log`:**
```
du -sh /var/log/* 2>/dev/null | sort -h | tail -5
```
**Output:** `/var/log/journal` was the largest at 5.3 GB — consuming the most space.

**Look at a config file in `/etc`:**
```
cat /etc/hostname
```
**Output:** `svdi-u12q-x-036` — the hostname of the machine.

**Check the home directory:**
```
ls -la ~
```
**Output:** Lists all files, including hidden ones.

---

## Part 2: Scenario-Based Practice

### Scenario 1: Service Not Starting
*A web application service called `myapp` failed to start after a server reboot. What commands would you run to diagnose the issue?*

1. Check whether the service is running:
   ```
   systemctl status myapp
   ```
2. Check the logs:
   ```
   journalctl -u myapp -n 50
   ```
3. Since it's not starting after reboot, check whether it's enabled to auto-start on boot:
   ```
   systemctl is-enabled myapp
   ```
4. If not enabled, enable it:
   ```
   systemctl enable myapp
   ```
5. Restart the service:
   ```
   systemctl restart myapp
   ```

---

### Scenario 2: High CPU Usage
*Your manager reports the application server is slow. You SSH in — what commands identify which process is using high CPU?*

1. Get a live view of all processes:
   ```
   top
   ```
2. If the output is too messy to parse, sort directly by CPU usage:
   ```
   ps aux --sort=-%CPU | head -10
   ```
3. Note the PID of the offending process, investigate why it's consuming so much CPU, then kill/stop it if needed:
   ```
   kill <PID>
   ```

---

### Scenario 3: Finding Service Logs
*A developer asks: "Where are the logs for the `docker` service?" It's managed by systemd.*

1. Check the service status:
   ```
   systemctl status docker
   ```
2. Pull the logs — this is the main ask:
   ```
   journalctl -u docker -n 50
   ```
3. If the team needs to watch logs live:
   ```
   journalctl -u docker -f
   ```

---

### Scenario 4: File Permissions Issue
*A script at `/home/user/backup.sh` won't execute. Running `./backup.sh` returns "Permission denied."*

1. Grant execute permission:
   ```
   chmod +x backup.sh
   ```
2. Verify the permission change:
   ```
   ls -l /home/user/backup.sh
   ```
   Before: `-rw-r--r--` → After: `-rwxr-xr-x` — note the added `x`, confirming execute permission is now granted.
