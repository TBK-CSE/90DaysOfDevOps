# Day 12 – Breather & Revision (Days 01–11)

## Goal
Take a one-day pause to consolidate everything from Days 01–11 so the fundamentals stick.

---

## Key Commands Revisited

| Command | Purpose |
|---|---|
| `ps aux` | Check running processes |
| `systemctl status nginx` | Check service status |
| `journalctl -u nginx` | Check logs |

## File Operations Practice

| Command | Purpose |
|---|---|
| `echo "test" >> file.txt` | Append content |
| `chmod 755 script.sh` | Change permissions |
| `chown user:group file` | Change ownership |

## Top 5 Go-To Commands
1. `ps aux`
2. `top`
3. `systemctl status`
4. `journalctl`
5. `chmod`

## User/Group Practice
- Created a user and checked with `id`
- Changed file ownership and verified with `ls -l`

---

## Self Check

### 1. Three most useful commands
- `ps aux` → quick process check
- `top` → live CPU usage
- `journalctl` → logs debugging

**Remember:**
- `du -h` → disk usage of files/folders (e.g. `du -h /var/log`)
- `df -h` → disk usage of the whole filesystem

### 2. How to check service health
```
systemctl status nginx
journalctl -u nginx
ps aux | grep nginx
```

### 3. Safe permission/ownership change
```
chmod 755 script.sh
chown user:group file.txt
```

### 4. Focus for the next 3 days
- Improve troubleshooting speed
- Practice more real-world scenarios
- Get comfortable with logs and debugging
