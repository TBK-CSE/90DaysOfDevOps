# Day 03 – Linux Commands Practice

**Goal:** Build Linux command confidence — focus on process management, filesystem, networking troubleshooting.

## File System Commands

| Command | What it does |
|---|---|
| `ls` | List files in current dir; `-l` for long listing (permissions, size, owner) |
| `cd /path` | Navigate to path; `cd ..` goes up one dir; `cd` alone goes to home/root |
| `mkdir folder_name` | Create a folder; `rm -rf path` removes it (and contents, forcefully) |
| `cp SRC DEST` | Copy SRC to DEST |
| `mv SRC DEST` | Move file/dir to destination; also used to rename (`mv file1.txt file2.txt`) |
| `cat file.txt` | Print file contents to terminal |
| `grep -r "you" .` | Search for "you" in current dir; `-r` searches subfolders too |
| `chmod 755 script.sh` | Set permissions — owner: read/write/execute, group & others: read/execute (4=read, 2=write, 1=execute) |
| `chown user:user file` | Change file's owner and group to `user` |
| `df -h` | Show disk (storage) usage — not CPU, not RAM |
| `du -sh folder/` | Show total size of a folder |

## Process Management Commands

| Command | What it does |
|---|---|
| `ps aux` | List all running processes with CPU/memory usage |
| `top` | Real-time, live-updating version of `ps aux` |
| `kill -9 1234` | Force-kill process with PID 1234. Signal reference: `15` graceful stop (default), `9` force kill (can't be ignored), `2` interrupt (like Ctrl+C), `19` pause, `18` resume |

## Networking Troubleshooting

| Command | What it does |
|---|---|
| `ping www.google.com` | Test connectivity to a host |
| `ip addr` | Show IP addresses and network interfaces |
| `curl -I https://ex.com` | Fetch HTTP headers to test an endpoint |
| `dig google.com` | Get DNS resolution details (resolve domain to IP) |
| `netstat -tulnp` | Show open ports and listening services (e.g. `tcp 0.0.0.0:80 LISTEN 1234/nginx` → port 80 on nginx) |
| `traceroute google.com` | Show request's path across the internet, hop by hop through routers |
