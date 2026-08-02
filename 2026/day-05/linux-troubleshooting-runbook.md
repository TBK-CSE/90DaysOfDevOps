# Day 05 – Linux Troubleshooting Drill: CPU, Memory, and Logs

## Task
Run a focused troubleshooting drill on a target service, capture a health snapshot, trace logs, and write a mini runbook.

## Target Service
**ssh** — chosen as the service to inspect for this drill.

---

## Environment Basics

**`uname -a`**
Shows system kernel details.

![uname -a output]<img width="1111" height="81" alt="image" src="https://github.com/user-attachments/assets/362da2e7-5d67-4961-9845-9e827c931fb4" />


**`cat /etc/os-release`**
Shows OS-related information.

![cat /etc/os-release output]<img width="928" height="236" alt="image" src="https://github.com/user-attachments/assets/03397888-e541-4236-872a-d08081d59d31" />


---

## Filesystem Sanity Check

**`mkdir /tmp/runbook-demo_1 && cp /etc/hosts /tmp/runbook-demo_1/hosts-copy && ls -l /tmp/runbook-demo_1`**
Created a throwaway folder, copied `/etc/hosts` into it, and listed the result to confirm the copy succeeded.

![mkdir and cp filesystem sanity check]<img width="1561" height="486" alt="02-mkdir-cp-filesystem-sanity" src="https://github.com/user-attachments/assets/5e8e5ac3-8560-4a35-a809-c7f65b84c70d" />


**`lsblk` / `lvm` / `pvs` / `pvcreate`**
Checked block device layout (disks, partitions, mount points) and explored LVM tooling (physical volumes) as a bonus disk-layout check.

![lsblk and lvm exploration]<img width="623" height="310" alt="01-lsblk-lvm" src="https://github.com/user-attachments/assets/893b2722-6635-48c0-8baa-3f7733c3f916" />


---

## Process Check

**`ps -o pid`**
Quick PID lookup for the target service's running instances.

![ps -o pid output]<img width="1571" height="309" alt="05-ps-o-pid" src="https://github.com/user-attachments/assets/d071a3b7-3342-4620-84b2-7806751f84a8" />


---

## Snapshot: CPU & Memory

**`top -b -n 1`**
Batch mode (`-b`), single run (`-n 1`) — without `-n`, `top` would run continuously in the background. CPU shows mostly idle, no load spikes; system is calm.

![top batch mode]<img width="1522" height="964" alt="03-top-batch-mode" src="https://github.com/user-attachments/assets/6b29d53f-dd89-45d0-893e-1c0f3351ad5e" />


**`htop`**
Interactive, color-coded view of the same data — processes, per-core CPU bars, memory usage. Confirms the same picture: nothing abnormal running.

![htop interactive view]<img width="1608" height="968" alt="04-htop" src="https://github.com/user-attachments/assets/f410b01d-3b6b-4c19-91cc-3fc6a5c376bb" />


**`free -h`**
Memory (RAM) usage in human-readable form. Total, used, free, and available memory all look healthy — no memory pressure observed.

![free -h output]<img width="1121" height="334" alt="06-free-h" src="https://github.com/user-attachments/assets/91bcf7d9-75dc-4ae8-9440-a5022b5c89c7" />


---

## Snapshot: Disk & IO

**`df -h`**
Disk (storage) usage across mounted filesystems — root partition has comfortable free space, no volume close to full.

![df -h output]<img width="804" height="309" alt="07-df-h" src="https://github.com/user-attachments/assets/ff175203-29cb-47b8-812a-23b28a08dc50" />


**`du -sh /var/log`**
Total size of the `/var/log` directory — `-s` for summary, `-h` for human-readable units. Log directory size is small and not a concern.

![du -sh /var/log output]<img width="1289" height="246" alt="08-du-sh-varlog" src="https://github.com/user-attachments/assets/281b6a86-75fc-4eb1-bd57-3bdb6789cf64" />


**`iostat`**
Disk I/O statistics — read/write throughput per device. No unusual I/O wait or saturation on any device.

![iostat output]<img width="969" height="330" alt="09-iostat" src="https://github.com/user-attachments/assets/046739e0-912f-43a9-9664-71ae44257162" />


> **Note:** `df` = total disk usage across the filesystem, `du` = size of a specific folder.

---

## Snapshot: Network

**`ss -tulpn`**
Lists listening ports and the processes bound to them. `-t` TCP, `-u` UDP, `-l` listening only, `-p` show process, `-n` numeric (skip DNS lookups). Confirms ssh is listening on port 22.

![ss -tulpn output]<img width="1773" height="264" alt="10-ss-tulpn" src="https://github.com/user-attachments/assets/c5f133e9-60a6-4b07-9718-984e2024706e" />


**`netstat -tulpn`**
Same information via the older `netstat` tool, used as a cross-check against `ss`.

![netstat -tulpn output]<img width="1009" height="291" alt="11-netstat-tulpn" src="https://github.com/user-attachments/assets/d68f40a6-17db-496d-ae51-d66f2b4b584d" />


**`ping google.com`**
Confirms basic outbound network connectivity — replies coming back consistently with low latency.

![ping google.com output]<img width="879" height="239" alt="12-ping-google" src="https://github.com/user-attachments/assets/ae9493d8-798c-4608-94aa-15e0a95b92e3" />


**`curl -I http://www.google.com`**
Sends an HTTP request and shows only the response headers (`-I`). Got a clean `200 OK`, confirming the box can reach the internet over HTTP.

![curl -I http://www.google.com output]<img width="1843" height="357" alt="13-curl-I-google" src="https://github.com/user-attachments/assets/a7e3dfca-1c62-4c46-93de-bc9679e623fe" />


---

## Logs Reviewed

**`tail -20 /var/log/syslog`**
Last 20 lines of the general system log. Shows routine background activity (scheduled jobs, service starts) — nothing indicating a failure.

![tail -20 /var/log/syslog output]<img width="1848" height="542" alt="14-tail-syslog" src="https://github.com/user-attachments/assets/a6715b28-5f51-42ec-a129-2c6f0d48cb45" />


**`journalctl -u ssh -n 20`**
Last 20 log lines specific to the ssh service (`-u` = unit). Shows a mix of successful key-based logins. `systemctl` is for managing the service (start/stop/restart); `journalctl` is for reviewing its history and logs.

![journalctl -u ssh -n 20 output]<img width="1855" height="363" alt="15-journalctl-ssh" src="https://github.com/user-attachments/assets/0b619cfe-8029-4508-a633-9aecead09327" />


---

## Quick Findings

- System is stable
- No high CPU or memory usage
- SSH service is running and reachable on port 22
- No critical errors in logs — only routine activity

## If This Worsens (Next Steps)

1. Restart the ssh service: `systemctl restart ssh`
2. Pull detailed diagnostic logs: `journalctl -xe`
3. Monitor CPU continuously: `top` (without `-n 1`)
4. Check who's currently logged in: `who`
5. Resolve a suspicious login IP: `nslookup <IP-address>`
6. Escalate to the team immediately if the issue persists
