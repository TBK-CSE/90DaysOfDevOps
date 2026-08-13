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
<img width="673" height="296" alt="image" src="https://github.com/user-attachments/assets/7108b697-ba82-479e-acab-190eeffd159e" />
<img width="503" height="257" alt="image" src="https://github.com/user-attachments/assets/541deed1-fe12-4364-a810-08cd589b4175" />


---

## Task 2: While Loop

`countdown.sh`:
- Takes a number from the user
- Counts down to 0 using a while loop
- Prints "Done!" at the end

<img width="575" height="470" alt="image" src="https://github.com/user-attachments/assets/213da7f1-3597-4274-bd61-95e6691e428e" />


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

<img width="464" height="173" alt="image" src="https://github.com/user-attachments/assets/62f35b50-cfae-4889-bab9-39f874a3eb3d" />

<img width="929" height="308" alt="image" src="https://github.com/user-attachments/assets/4eff1947-c918-426f-8ba4-3e0ad6abe96a" />


---

## Task 4: Install Packages via Script

`install_packages.sh`:
- Defines a package list: `nginx`, `curl`, `wget`
- Loops through the list
- Checks if each is installed (`dpkg -s` or `rpm -q`)
- Installs if missing, skips if already present
- Prints status for each package

> Run as root: `sudo -i` or `sudo su`

<img width="630" height="382" alt="image" src="https://github.com/user-attachments/assets/dfc81295-4a54-466d-8b13-75df5fdf18be" />



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
<img width="813" height="276" alt="image" src="https://github.com/user-attachments/assets/e6e4bc3f-262e-454b-8eee-b11da519e96f" />

**2.** Modified `install_packages.sh` to check if it's being run as root — exits with a message if not.
<img width="790" height="440" alt="image" src="https://github.com/user-attachments/assets/446528cb-d93a-464c-84e2-4de12bdb1cb1" />



---

## Scripts Created
`for_loop.sh`, `count.sh`, `countdown.sh`, `greet.sh`, `args_demo.sh`, `install_packages.sh`, `safe_script.sh`

## What I Learned
- How to use loops in scripting
- How to pass arguments to scripts
- Basic automation and error handling
