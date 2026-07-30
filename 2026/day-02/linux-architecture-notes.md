# Day 02 – Linux Architecture, Processes, systemd 

## Origin
1991. Linus Torvalds hate MINIX + MS-DOS limits. Build own Unix-like OS for 80386 PC. Make open-source → code free, anyone read/change/modify any file.

## Architecture — remember ASK
- **A** = Application
- **S** = Shell
- **K** = Kernel

Flow: Hardware (CPU, RAM) → Kernel (talk to hardware) → Shell (take cmd, send to kernel) → Application (Chrome, terminal, etc).

## Boot + Process Creation
Power on → BIOS wake motherboard → loads GRUB → GRUB load Linux kernel → kernel spawn PID 1 = init/systemd (system + daemon = background service).

Everything in Linux = process. Example:
```
cp folder1 folder2
```
`cp` = binary in `/bin`, contains C code, runs → becomes process, gets PID.

Check processes:
```
ps aux            # list all process
ps aux | grep mv  # filter by name
top                # live view
```

## Filesystem — everything = file or process
Think octopus: root (/) = head, sub-folders = arms.

| Path | Role |
|---|---|
| `/` | root, start of everything |
| `/root` | home dir for root user (superuser) |
| `/bin` | user binaries, common cmds, single-user mode too |
| `/sbin` | sysadmin binaries (iptables, reboot, fdisk, ifconfig, swapon) |
| `/dev` | device files (tty1, usbmon0...) |
| `/var` | growing data: `/var/log` logs, `/var/lib` db/pkg, `/var/mail` mail, `/var/tmp` temp-till-reboot |
| `/mnt` | temp mount point |
| `/media` | removable media mount |
| `/usr` | user apps/files (not system) |
| `/etc` | config files, startup/shutdown scripts |
| `/boot` | GRUB + kernel files |
| `/opt` | 3rd-party optional apps |
| `/home` | user home dirs |
| `/tmp` | temp files, wiped on reboot |

## systemd — why matter
First user-space process. Start/stop/check any service.
```
systemctl start nginx   # systemctl = control tool for systemd
```

## Process States
| Code | State | Meaning |
|---|---|---|
| R | Running | on CPU or waiting for CPU turn (1 process/core at a time) |
| S | Sleeping | wait for event (input, net, disk) |
| D | Uninterruptible Sleep | wait on disk/kernel I/O, can't interrupt |
| T | Stopped | paused by signal (e.g. Ctrl+Z) |
| Z | Zombie | done running, parent not read exit status yet, dead but entry stays |

## Top 5 Daily Commands
1. `grep -r "string" /path` → find matching lines
2. `ls -a` → list files/dirs (incl hidden)
3. `cd` → change dir
4. `crontab -e` → edit cron schedule file
5. `chmod +x file` → toggle execute permission
