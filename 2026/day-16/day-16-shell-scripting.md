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
<img width="842" height="367" alt="image" src="https://github.com/user-attachments/assets/3bf4a700-cc03-4c14-b549-17839b9db445" />
<img width="632" height="340" alt="image" src="https://github.com/user-attachments/assets/c5c2166e-f896-4fce-9605-0656662974c0" />


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
   
<img width="462" height="122" alt="image" src="https://github.com/user-attachments/assets/11e947d0-2cb8-4184-9d1f-8fb3ed3ae28b" />
<img width="659" height="192" alt="image" src="https://github.com/user-attachments/assets/4bdf1ec0-8b05-4009-95ef-08094eff8ace" />


---

## Task 3: User Input with `read`

1. Create `greet.sh` that:
   - Asks the user for their name using `read`
   - Asks for their favourite tool
   - Prints: `Hello <name>, your favourite tool is <tool>`

<img width="617" height="137" alt="image" src="https://github.com/user-attachments/assets/85254548-3431-444e-94b2-111a3aef9991" />
<img width="621" height="142" alt="image" src="https://github.com/user-attachments/assets/e7d59918-68f6-46ad-8326-41bb87f9a20d" />


**Note:** `-p` prints a prompt message before reading input.

---

## Task 4: If-Else Conditions

**Part 1 — `check_number.sh`:**
- Takes a number using `read`
- Prints whether it's **positive**, **negative**, or **zero**

<img width="386" height="173" alt="image" src="https://github.com/user-attachments/assets/6e7881e2-5691-427b-8ddf-681d9a733e1b" />
<img width="699" height="214" alt="image" src="https://github.com/user-attachments/assets/a4d961df-8bfc-42f9-a588-8fd4332af232" />


**Part 2 — `file_check.sh`:**
- Asks for a filename
- Checks if the file **exists** using `-f`
- Prints an appropriate message

<img width="853" height="441" alt="image" src="https://github.com/user-attachments/assets/232387da-104d-4143-9436-34eea1ba10bf" />


---

## Task 5: Combine It All

Create `server_check.sh` that:
1. Stores a service name in a variable (e.g. `nginx`, `sshd`)
2. Asks: "Do you want to check the status? (y/n)"
3. If `y` — runs `systemctl status <service>` and prints whether it's **active** or **not**
4. If `n` — prints "Skipped."

<img width="1441" height="808" alt="image" src="https://github.com/user-attachments/assets/d8ae3f08-ad32-4a6c-acd6-6caeac93f7f3" />
<img width="1249" height="891" alt="image" src="https://github.com/user-attachments/assets/5444946d-c3e5-4aa4-b75b-ad3dfcd5dfc4" />


---

## Summary

**Scripts Created**
`hello.sh`, `variables.sh`, `greet.sh`, `check_number.sh`, `file_check.sh`, `server_check.sh`

**What I Learned**
- How to write basic shell scripts
- How to use variables
- How to take user input
- How to use if-else conditions
