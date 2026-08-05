# Day 10 – Linux File Permissions & File Operations

## Overview
Master the fundamentals of Linux file permissions and basic file operations through hands-on practice.

### Learning Objectives
- Create and read files using command-line tools (touch, cat, vim, echo)
- Understand Linux permission structure (rwx format)
- Modify file and directory permissions using chmod
- Troubleshoot permission-related errors

---

## Phase 1: File Creation (10 minutes)

### Task 1.1 – Create Files
**Objective:** Set up the initial file structure

**Commands:**
```bash
# Create an empty file
touch devops.txt

# Create a file with content
echo "My DevOps notes" > notes.txt

# Create and edit a shell script
vim script.sh
# Add content: echo "Hello DevOps"
```
<img width="864" height="115" alt="image" src="https://github.com/user-attachments/assets/086a2fde-a800-4f6c-9157-892ca153c5e6" />
<img width="534" height="155" alt="image" src="https://github.com/user-attachments/assets/d8a92ef9-840c-4830-852e-f55ed69d6cfe" />


**Verification:**
```bash
ls -l
```
<img width="695" height="384" alt="image" src="https://github.com/user-attachments/assets/3ce6b1b7-4ee2-4fe0-a41e-fe35d4a5f666" />


**Output Format:**
```
-rw-r--r-- 1 user group 0 Nov 15 10:30 devops.txt
-rw-r--r-- 1 user group 18 Nov 15 10:31 notes.txt
-rw-r--r-- 1 user group 24 Nov 15 10:32 script.sh
```

---

## Phase 2: File Reading (10 minutes)

### Task 2.1 – Read Files
**Objective:** Access and display file contents

**Commands:**
```bash
# Display full file content
cat notes.txt

# View file in read-only mode (vim)
vim -R script.sh

# Display first 5 lines of a system file
head -5 /etc/passwd

# Display last 5 lines of a system file
tail -5 /etc/passwd
```
<img width="508" height="243" alt="image" src="https://github.com/user-attachments/assets/5ad67e97-08b4-4f31-997a-a1221b51252b" />

---

## Phase 3: Understanding Permissions (10 minutes)

### Permission Structure

Linux file permissions follow this format:
```
rwxrwxrwx
│││││││││
│││││││└─ Others: execute
││││││└── Others: write
│││││└─── Others: read
││││└──── Group: execute
│││└───── Group: write
││└────── Group: read
│└─────── Owner: execute
└──────── Owner: read
```

### Permission Categories

| Symbol | Value | Meaning |
|--------|-------|---------|
| r | 4 | Read – view file contents |
| w | 2 | Write – modify file contents |
| x | 1 | Execute – run as program |

### User Categories

| Symbol | Meaning |
|--------|---------|
| u | User (owner) |
| g | Group |
| o | Others |
| a | All (user + group + others) |

### Example Permission Breakdown

**File:** `notes.txt` with permissions `640`
- **6** (Owner): read (4) + write (2) = 6
- **4** (Group): read = 4
- **0** (Others): no permissions = 0

---

## Phase 4: Modifying Permissions (20 minutes)

### Task 4.1 – Apply Permission Changes

**Requirement 1:** Make script.sh executable
```bash
chmod u+x script.sh
# Or using numeric: chmod 755 script.sh
# Verification: ./script.sh
```

**Requirement 2:** Make devops.txt read-only (remove write from all)
```bash
chmod a-w devops.txt
# Verification: ls -l devops.txt
# Result: -r--r--r--
```

**Requirement 3:** Set notes.txt to 640 (owner: rw, group: r, others: none)
```bash
chmod 640 notes.txt
# Verification: ls -l notes.txt
# Result: -rw-r----- 
```

**Requirement 4:** Create directory with 755 permissions
```bash
mkdir project
chmod 755 project
# Verification: ls -ld project
# Result: drwxr-xr-x
```

### chmod Syntax Reference

**Symbolic Method:**
```bash
chmod [who][operation][permission] filename
# who:       u (user), g (group), o (others), a (all)
# operation: + (add), - (remove), = (set exactly)
# permission: r, w, x
```

**Examples:**
```bash
chmod a-w script.sh    # Remove write from all
chmod u+x notes.txt    # Add execute for owner
chmod 644 file.txt     # Set to rw-r--r--
```

**Numeric Method:**
```bash
chmod [owner][group][others] filename
# Each digit is sum of: r(4) + w(2) + x(1)
```

---

## Phase 5: Testing & Troubleshooting (10 minutes)

### Task 5.1 – Test Permission Behavior

**Test 1:** Write to a read-only file
```bash
echo "test" >> devops.txt
# Expected Error: bash: devops.txt: Permission denied
```

**Test 2:** Execute a file without execute permission
```bash
./notes.txt
# Expected Error: Permission denied
```

**Test 3:** Execute with proper permissions
```bash
./script.sh
# Expected Output: Hello DevOps
```<img width="584" height="126" alt="image" src="https://github.com/user-attachments/assets/19c9d038-f234-4d70-a943-448d344b269a" />
<img width="538" height="89" alt="image" src="https://github.com/user-attachments/assets/773c9ca6-cc54-4165-baab-0d84f8de4320" />

<img width="521" height="85" alt="image" src="https://github.com/user-attachments/assets/8c66383f-2f7b-477a-825d-958ec237bae0" />
<img width="914" height="455" alt="image" src="https://github.com/user-attachments/assets/2f1b7300-167a-4519-ba79-8482a91703db" />
<img width="914" height="455" alt="image" src="https://github.com/user-attachments/assets/5250aa01-facd-47a6-8a10-526d7cdf641a" />




**Key Insight:**
Permissions control whether operations are allowed. Without appropriate permissions, the system denies access regardless of file content.

---

## Summary

### Files Created
| File | Type | Purpose |
|------|------|---------|
| `devops.txt` | Empty file | Practice read-only permissions |
| `notes.txt` | Text file | Practice numeric permissions (640) |
| `script.sh` | Executable | Practice execute permissions |
| `project/` | Directory | Practice directory permissions (755) |

### Key Commands Mastered
```
touch    – Create empty files
cat      – Display file contents
vim      – Create and edit files
echo     – Output text
ls -l    – List files with detailed permissions
chmod    – Change file permissions
head/tail – View file portions
```

### Core Concepts
1. **rwx Format:** Owner → Group → Others (each has read/write/execute)
2. **Numeric Values:** Read (4), Write (2), Execute (1)
3. **chmod Usage:** Change permissions symbolically or numerically
4. **Permission Impact:** Controls who can read, write, and execute files
5. **Error Handling:** Permission denied errors guide debugging

### What You've Learned
✓ Create files and directories  
✓ Read and display file contents  
✓ Interpret Linux permission notation  
✓ Modify permissions using chmod  
✓ Understand permission effects on access  
✓ Troubleshoot permission-related errors  

---

## Next Steps
- Practice with different permission combinations
- Explore special permissions (setuid, setgid, sticky bit)
- Learn about umask and default permissions
- Apply permissions to real project structures
