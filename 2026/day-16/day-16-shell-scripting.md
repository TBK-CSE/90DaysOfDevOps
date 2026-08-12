# Day 16 – Shell Scripting Basics

## Task
Start the shell scripting journey — learn the fundamentals every script needs.

**Covers:**
- Understanding the **shebang** (`#!/bin/bash`) and why it matters
- Working with **variables**, `echo`, and `read`
- Writing basic **if-else** conditions

---

## Task 1: Your First Script

1. Create `hello.sh`
2. Add the shebang line `#!/bin/bash` at the top
3. Print `Hello, DevOps!` using `echo`
4. Make it executable and run it

*[screenshot: hello.sh script and output]*

**What happens if you remove the shebang line?**
The script still ran — because it fell back to the default shell (`sh`), and `sh` supported the syntax used here.

**So why bother with a shebang?** If a script is written specifically for `bash`, some commands or keywords may not work under `sh`. The shebang explicitly tells the system which interpreter to use. Without it, the system falls back to its default interpreter (`sh`).

---

## Task 2: Variables

1. Create `variables.sh` with:
   - A variable for `NAME`
   - A variable for `ROLE` (e.g. "DevOps Engineer")
   - Print: `Hello, I am <NAME> and I am a <ROLE>`
2. Compare single quotes vs double quotes

*[screenshot: variables.sh — single vs double quote behavior]*

---

## Task 3: User Input with `read`

1. Create `greet.sh` that:
   - Asks the user for their name using `read`
   - Asks for their favourite tool
   - Prints: `Hello <name>, your favourite tool is <tool>`

*[screenshot: greet.sh script]*
*[screenshot: greet.sh output]*

**Note:** `-p` prints a prompt message before reading input.

---

## Task 4: If-Else Conditions

**Part 1 — `check_number.sh`:**
- Takes a number using `read`
- Prints whether it's **positive**, **negative**, or **zero**

*[screenshot: check_number.sh script]*
*[screenshot: check_number.sh output]*

**Part 2 — `file_check.sh`:**
- Asks for a filename
- Checks if the file **exists** using `-f`
- Prints an appropriate message

*[screenshot: file_check.sh script]*
*[screenshot: file_check.sh output]*

---

## Task 5: Combine It All

Create `server_check.sh` that:
1. Stores a service name in a variable (e.g. `nginx`, `sshd`)
2. Asks: "Do you want to check the status? (y/n)"
3. If `y` — runs `systemctl status <service>` and prints whether it's **active** or **not**
4. If `n` — prints "Skipped."

*[screenshot: server_check.sh script]*
*[screenshot: server_check.sh output]*

---

## Summary

**Scripts Created**
`hello.sh`, `variables.sh`, `greet.sh`, `check_number.sh`, `file_check.sh`, `server_check.sh`

**What I Learned**
- How to write basic shell scripts
- How to use variables
- How to take user input
- How to use if-else conditions
