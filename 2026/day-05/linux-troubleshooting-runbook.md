# Day 05 – Linux Troubleshooting Drill: CPU, Memory, and Logs

## Task
Run a focused troubleshooting drill on a target service, capture a health snapshot, trace logs, and write a mini runbook.

## Target Service
**ssh** — chosen as the service to inspect for this drill.

---

## Environment Basics

**`uname -a`**
Shows system kernel details.

![uname -a output](https://github.com/user-attachments/assets/62d82afd-b387-4caa-8de9-d26052ee1d91)

**`cat /etc/os-release`**
Shows OS-related information.

![cat /etc/os-release output](https://github.com/user-attachments/assets/e9329f9e-0e7c-47ff-9436-cf200601d9b0)

---

## Filesystem Sanity Check

**`mkdir /tmp/runbook-demo_1 && cp /etc/hosts /tmp/runbook-demo_1/hosts-copy && ls -l /tmp/runbook-demo_1`**
Created a throwaway folder, copied `/etc/hosts` into it, and listed the result to confirm the copy succeeded.

![mkdir and cp filesystem sanity check](day-05-images/02-mkdir-cp-filesystem-sanity.png)

**`lsblk` / `lvm` / `pvs` / `pvcreate`**
Checked block device layout (disks, partitions, mount points) and explored LVM tooling (physical volumes) as a bonus disk-layout check.

![lsblk and lvm exploration](day-05-images/01-lsblk-lvm.png)

---

## Process Check

**`ps -o pid`**
Quick PID lookup for the target service's running instances.

![ps -o pid output](day-05-images/05-ps-o-pid.png)

---

## Snapshot: CPU & Memory

**`top -b -n 1`**
Batch mode (`-b`), single run (`-n 1`) — without `-n`, `top` would run continuously in the background. CPU shows mostly idle, no load spikes; system is calm.

![top batch mode](day-05-images/03-top-batch-mode.png)

**`htop`**
Interactive, color-coded view of the same data — processes, per-core CPU bars, memory usage. Confirms the same picture: nothing abnormal running.

![htop interactive view](day-05-images/04-htop.png)

**`free -h`**
Memory (RAM) usage in human-readable form. Total, used, free, and available memory all look healthy — no memory pressure observed.

![free -h output](day-05-images/06-free-h.png)

---

## Snapshot: Disk & IO

**`df -h`**
Disk (storage) usage across mounted filesystems — root partition has comfortable free space, no volume close to full.

![df -h output](day-05-images/07-df-h.png)

**`du -sh /var/log`**
Total size of the `/var/log` directory — `-s` for summary, `-h` for human-readable units. Log directory size is small and not a concern.

![du -sh /var/log output](day-05-images/08-du-sh-varlog.png)

**`iostat`**
Disk I/O statistics — read/write throughput per device. No unusual I/O wait or saturation on any device.

![iostat output](day-05-images/09-iostat.png)

> **Note:** `df` = total disk usage across the filesystem, `du` = size of a specific folder.

---

## Snapshot: Network

**`ss -tulpn`**
Lists listening ports and the processes bound to them. `-t` TCP, `-u` UDP, `-l` listening only, `-p` show process, `-n` numeric (skip DNS lookups). Confirms ssh is listening on port 22.

![ss -tulpn output](day-05-images/10-ss-tulpn.png)

**`netstat -tulpn`**
Same information via the older `netstat` tool, used as a cross-check against `ss`.

![netstat -tulpn output](day-05-images/11-netstat-tulpn.png)

**`ping google.com`**
Confirms basic outbound network connectivity — replies coming back consistently with low latency.

![ping google.com output](day-05-images/12-ping-google.png)

**`curl -I http://www.google.com`**
Sends an HTTP request and shows only the response headers (`-I`). Got a clean `200 OK`, confirming the box can reach the internet over HTTP.

![curl -I http://www.google.com output](day-05-images/13-curl-I-google.png)

---

## Logs Reviewed

**`tail -20 /var/log/syslog`**
Last 20 lines of the general system log. Shows routine background activity (scheduled jobs, service starts) — nothing indicating a failure.

![tail -20 /var/log/syslog output](day-05-images/14-tail-syslog.png)

**`journalctl -u ssh -n 20`**
Last 20 log lines specific to the ssh service (`-u` = unit). Shows a mix of successful key-based logins. `systemctl` is for managing the service (start/stop/restart); `journalctl` is for reviewing its history and logs.

![journalctl -u ssh -n 20 output](day-05-images/15-journalctl-ssh.png)

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
