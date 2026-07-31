# Day 04 – Linux Practice: Processes and Services

**Goal:** Practice Linux fundamentals with real, hands-on commands.

## Section 1: Process checks

**`ps aux`**
Lists all running processes along with their CPU and memory usage.

**`ps aux | awk '{print $2, $11}'`**
Extracts just the PID and service name from the process list.

**`top`**
Shows real-time CPU and memory usage, live-updating. Output can be piped and sorted further using `|` and arguments.

## Section 2: Service checks (systemd)

**`systemctl status ssh`**
Shows the current status of a service — whether it's active, inactive, or stopped.

**`systemctl list-unit --type=service | head -10`**
Lists currently running units of type "service."
- Without `--type=service`, it lists *all* unit types — services, mounts, sockets, timers, etc.
- Without `list-unit`, `systemctl` alone just prints general command usage/help — similar to running `npm` with no arguments.

## Section 3: Log checks

**`journalctl -u ssh | tail -10`**
Shows logs for the ssh service — login attempts, failures, successes — filtered by `-u` (unit), with only the last 10 lines shown.
- Note: `systemctl` is for managing a service (start/stop/restart). For logs and event history, use `journalctl` instead.

**`tail -n 10 /var/log/syslog`**
Shows the last 10 lines of `/var/log/syslog` — the general system log, capturing what's happening across the system.

The ssh service was already inspected in the sections above.
