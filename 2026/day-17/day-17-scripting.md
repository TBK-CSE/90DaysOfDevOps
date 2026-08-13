# Day 17 – Shell Scripting: Loops, Arguments & Error Handling

## Task
Level up scripting skills — loops, command-line arguments, and error handling.

**Covers:**
- Writing **for** and **while** loops
- Using **command-line arguments** (`$1`, `$2`, `$#`, `$@`)
- Installing packages via script
- Adding basic **error handling**

---

## Task 1: For Loop

1. `for_loop.sh` — loops through a list of 5 fruits and prints each one
2. `count.sh` — prints numbers 1 to 10 using a for loop

*[screenshot: for_loop.sh script]*
*[screenshot: for_loop.sh output]*
*[screenshot: count.sh script]*
*[screenshot: count.sh output]*

---

## Task 2: While Loop

`countdown.sh`:
- Takes a number from the user
- Counts down to 0 using a while loop
- Prints "Done!" at the end

*[screenshot: countdown.sh script]*
*[screenshot: countdown.sh output]*

---

## Task 3: Command-Line Arguments

1. `greet.sh`:
   - Accepts a name as `$1`
   - Prints `Hello, <name>!`
   - If no argument passed, prints `Usage: ./greet.sh <name>`
2. `args_demo.sh`:
   - Prints total number of arguments (`$#`)
   - Prints all arguments (`$@`)
   - Prints the script name (`$0`)

*[screenshot: greet.sh script]*
*[screenshot: greet.sh output]*
*[screenshot: args_demo.sh script]*
*[screenshot: args_demo.sh output]*

---

## Task 4: Install Packages via Script

`install_packages.sh`:
- Defines a package list: `nginx`, `curl`, `wget`
- Loops through the list
- Checks if each is installed (`dpkg -s` or `rpm -q`)
- Installs if missing, skips if already present
- Prints status for each package

> Run as root: `sudo -i` or `sudo su`

*[screenshot: install_packages.sh script]*
*[screenshot: install_packages.sh output]*

**Bug found:** the `if` condition used `$pkg` instead of `$pkgs` — fixed.

---

## Task 5: Error Handling

**1. `safe_script.sh`:**
- Uses `set -e` at the top (exit on error)
- Creates directory `/tmp/devops-test`
- Navigates into it
- Creates a file inside
- Uses `||` to print an error if any step fails

Example:
```bash
mkdir /tmp/devops-test || echo "Directory already exists"
```

**2.** Modified `install_packages.sh` to check if it's being run as root — exits with a message if not.

*[screenshot: safe_script.sh script]*
*[screenshot: safe_script.sh output]*
*[screenshot: install_packages.sh root check]*
*[screenshot: root check output]*

---

## Scripts Created
`for_loop.sh`, `count.sh`, `countdown.sh`, `greet.sh`, `args_demo.sh`, `install_packages.sh`, `safe_script.sh`

## What I Learned
- How to use loops in scripting
- How to pass arguments to scripts
- Basic automation and error handling
