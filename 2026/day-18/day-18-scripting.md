# Day 18 – Shell Scripting: Functions & Intermediate Concepts

## Task
Write cleaner, reusable scripts — functions, strict mode, and real-world patterns.

**Covers:**
- Writing and calling **functions**
- Using `set -euo pipefail` for safer scripts
- Working with **return values** and **local variables**
- Building an intermediate, function-driven script

---

## Task 1: Basic Functions

`functions.sh`:
- Function `greet` — takes a name, prints `Hello, <name>!`
- Function `add` — takes two numbers, prints their sum
- Both functions called from the script
<img width="647" height="396" alt="image" src="https://github.com/user-attachments/assets/f97dab7e-8604-46c5-a78b-015bf88cbe04" />


---

## Task 2: Functions with Return Values

`disk_check.sh`:
- Function `check_disk` — checks disk usage of `/` using `df -h`
- Function `check_memory` — checks free memory using `free -h`
- Main section calls both and prints results

<img width="913" height="519" alt="image" src="https://github.com/user-attachments/assets/9e57b689-a052-4de4-9634-5bc3a61a5747" />


---

## Task 3: Strict Mode — `set -euo pipefail`

`strict_demo.sh` with `set -euo pipefail` at the top. Tested:
- An **undefined variable** (`set -u` behavior)
- A **failing command** (`set -e` behavior)
- A **piped command** where one part fails (`set -o pipefail` behavior)

<img width="764" height="320" alt="image" src="https://github.com/user-attachments/assets/9af15d99-d6cb-46c6-a9bd-c0e9169d78e3" />


**What each flag does:**
- `set -e` → exit immediately if any command fails
- `set -u` → error out on undefined variables
- `set -o pipefail` → fails the whole pipeline if any command in it (`|`) fails

---

## Task 4: Local Variables

`local_demo.sh`:
- A function using the `local` keyword for variables
- Demonstrates that `local` variables don't leak outside the function
- Compared against a function using regular (global) variables

<img width="608" height="338" alt="image" src="https://github.com/user-attachments/assets/94abded0-3003-4880-8c8c-af737f2a54ec" />


---

## Task 5: Build a Script — System Info Reporter

`system_info.sh` — everything driven by functions:
1. Print hostname and OS info
2. Print uptime
3. Print disk usage (top 5 by size)
4. Print memory usage
5. Print top 5 CPU-consuming processes
6. `main` function calling all of the above, with section headers
7. `set -euo pipefail` at the top for safety
<img width="1200" height="743" alt="image" src="https://github.com/user-attachments/assets/0b27fd56-2dc0-442d-9a7c-b8e72d7bcc21" />
<img width="1009" height="861" alt="image" src="https://github.com/user-attachments/assets/001e5d7a-3a4c-42ca-84ea-ce29ac66f7a1" />


---

## Scripts Created
`functions.sh`, `disk_check.sh`, `strict_demo.sh`, `local_demo.sh`, `system_info.sh`

## What I Learned
- How to use functions for cleaner scripts
- Importance of strict mode (`set -euo pipefail`)
- How to structure scripts well
