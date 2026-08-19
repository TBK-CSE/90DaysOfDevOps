# Day 21 – Shell Scripting Cheat Sheet: Personal Reference Guide

## Goal
Consolidate everything learned across the shell scripting days into a personal, quick-reference cheat sheet.

---

## Quick Reference

| Topic | Key Syntax | Example |
|---|---|---|
| Variable | `VAR="value"` | `NAME="DevOps"` |
| Argument | `$1`, `$2`, `$#`, `$@` | `./script.sh file.txt` |
| Exit Code | `$?`, `exit` | `echo $?` |
| If | `if [ condition ]; then` | `if [ -f file ]; then` |
| For loop | `for i in list; do` | `for i in 1 2 3; do` |
| While loop | `while [ cond ]; do` | `while read line; do` |
| Function | `name() { ... }` | `greet() { echo "Hi"; }` |
| File Check | `-f`, `-d`, `-e`, `-s` | `[ -f file.txt ]` |
| Grep | `grep pattern file` | `grep -i "error" log.txt` |
| Awk | `awk '{print $1}' file` | `awk -F: '{print $1}' /etc/passwd` |
| Sed | `sed 's/old/new/g' file` | `sed -i 's/foo/bar/g' config.txt` |
| Cut | `cut -d delim -fN` | `cut -d: -f1 file.txt` |
| Sort | `sort`, `-n`, `-r`, `-u` | `sort -nr file.txt` |
| Uniq | `uniq`, `-c` | `sort file \| uniq -c` |
| WC | `wc -l/-w/-c` | `wc -l file.txt` |
| Head/Tail | `head -n`, `tail -f` | `tail -f app.log` |
| Read | `read -p` | `read -p "Enter name: " name` |
| Date | `date +FORMAT` | `date +%Y-%m-%d` |
| Pipe | `\|` | `cat file \| grep error` |
| Redirect | `>`, `>>` | `echo hi > file.txt` |
| Debug | `set -x` | `set -x` |
| Safe Mode | `set -euo pipefail` | `set -euo pipefail` |

---

## 1. Basics

**Shebang (`#!/bin/bash`)**
Tells the system which interpreter to use to run the script. Without it, the system falls back to its default interpreter.

**Running a script**
- `chmod +x <file_name>` — grants execute permission (owner + group + others)
- `./script.sh` — runs the script directly
- `bash script.sh` — runs the script explicitly via bash

**Comments**
- `# this is a comment` — single line
- `echo "Hello" # inline comment` — inline, after a command

**Variables and quoting**
```bash
NAME="Vishal D"
echo $NAME     # expands but splits into words: Vishal D (two tokens)
echo "$NAME"   # expands, preserved as a single value: Vishal D
echo '$NAME'   # no expansion — prints literally: $NAME
```

**Reading user input**
```bash
read -p "Enter your name: " NAME
```
`-p` shows a prompt message before reading input.

**Command-line arguments**
| Variable | Meaning |
|---|---|
| `$0` | Script file name |
| `$1` | First argument passed (e.g. `./script.sh log.log`) |
| `$#` | Number of arguments passed |
| `$@` | All arguments |
| `$?` | Exit status of the last command |

---

## 2. Operators and Conditionals

**String comparisons**
```bash
[ "$a" = "$b" ]     # equal
[ "$a" != "$b" ]    # not equal
[ -z "$a" ]         # empty
[ -n "$a" ]         # not empty
```

**Integer comparisons**
```bash
[ $a -eq $b ]   # equal
[ $a -ne $b ]   # not equal
[ $a -lt $b ]   # less than
[ $a -gt $b ]   # greater than
[ $a -le $b ]   # less than or equal
[ $a -ge $b ]   # greater than or equal
```

**File test operators**
| Flag | Checks |
|---|---|
| `-f` | Is a regular file? |
| `-d` | Is a directory? |
| `-e` | Exists (any type — symlink, dir, file)? |
| `-r` | Readable? |
| `-w` | Writable? |
| `-x` | Executable? |
| `-s` | Exists and is not empty? |

**if / elif / else**
```bash
if [ -f text.txt ]; then
    echo "file exists"
elif [ -d text.txt ]; then
    echo "it's a directory"
else
    echo "not found"
fi
```

**Logical operators**
```bash
cmd1 && cmd2   # true only if both succeed
cmd1 || cmd2   # true if either succeeds
! cmd1         # NOT — true if cmd1 fails
```

**case / esac**
```bash
case $VAR in
  start) echo "started the process" ;;
  end)   echo "ended the process" ;;
  *)     echo "invalid" ;;
esac
```

---

## 3. Loops

**for loop (list-based)**
```bash
for i in 1 2 3 4 5; do
    echo $i
done
```

**for loop (C-style)**
```bash
for ((i=1; i<=5; i++)); do
    echo $i
done
```

**while loop**
```bash
i=1
while [ $i -le 5 ]; do
    echo $i
    ((i++))
done
```

**until loop**
```bash
i=1
until [ $i -gt 5 ]; do
    echo $i
    ((i++))
done
```

**Loop control**
- `break` — exits the entire loop
- `continue` — skips the current iteration, moves to the next

**Looping over files**
```bash
for file in *.log; do
    echo "processing file: $file"
    wc -l "$file"
done
```

**Looping over command output**
```bash
while read line; do
    echo "line: $line"
done
```
Reads input line by line and echoes it back.

---

## 4. Functions

**Defining and calling**
```bash
greet() {
    echo "Hello $1"
}

greet vishal
```

**Passing arguments**
`$1`, `$2`, etc. inside a function refer to that function's own arguments — same as script-level positional params.

**Return values**
- `return <code>` — returns a numeric exit status, doesn't print anything
- `echo "value"` — the common way to "return" data from a function (capture with `$(func)`)

**Local variables**
```bash
myfunc() {
    local name="Vishal"
}
```
`local` scopes the variable to the function only — it doesn't leak outside.

---

## 5. Text Processing Commands

**grep**
```bash
grep "error" file.txt         # search pattern
grep -i "error" file.txt      # ignore case
grep -r "error" /logs         # recursive search
grep -c "error" file.txt      # count matches
grep -n "error" file.txt      # show line numbers
grep -v "error" file.txt      # invert (exclude matches)
grep -E "error|fail" file.txt # multiple patterns (regex)
```

**awk**
```bash
awk '{ print $1 }' file                  # print column 1
awk '{ print $1, $3 }' file.txt          # print columns 1 and 3
awk -F "," '{ print $1 }' file.csv       # custom delimiter (comma)
awk '/error/ {print}' file.txt           # print only matching lines
awk 'BEGIN {print "Start"} {print $1} END {print "End"}' file.txt
```

**sed**
```bash
sed 's/error/warning/' file.txt      # replace first match per line (prints only, doesn't edit file)
sed 's/error/warning/g' file.txt     # replace all matches
sed '2d' file.txt                    # delete line 2
sed -i 's/error/warning/g' file.txt  # edit the file in place
```

**cut**
```bash
# root:x:0:0:root:/root:/bin/bash
# ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash

cut -d ":" -f1 file.txt
# Output:
# root
# ubuntu
```

**sort**
```bash
sort file.txt        # alphabetical
sort -n numbers.txt  # numeric (1, 10, 12, 23...)
sort -r file.txt      # reverse order
sort -u file.txt      # unique — duplicates collapsed to one
```

**uniq**
```bash
uniq file.txt      # remove consecutive duplicates
uniq -c file.txt   # count occurrences (e.g. 3 apple, 2 banana)
uniq -d file.txt   # show only duplicated lines
```

**tr**
```bash
echo "abc" | tr 'a' 'x'       # replace a → x
echo "abc" | tr 'a-z' 'A-Z'   # lowercase → uppercase
echo "a b c" | tr -d ' '      # delete spaces
```

**wc**
```bash
wc file.txt
# 3 7 44 file.txt  → 3 lines, 7 words, 44 characters

wc -l file.txt  # line count
wc -w file.txt  # word count
wc -c file.txt  # character count
```

**head / tail**
```bash
head -5 file.txt   # first 5 lines
tail -5 file.txt   # last 5 lines
tail -f file.txt   # follow mode (live log tailing)
```

---

## 6. Useful One-Liners

- Delete files older than 7 days: `find . -name "*.log" -mtime +7 -delete`
- Count lines across `.log` files: `wc -l *.log`
- Replace a string across multiple files: `sed -i "s/error/warning/g" *.log`
- Check if a service is running: `systemctl is-active nginx` or `systemctl status nginx`
- Alert on high disk usage: `df -h | awk '$5+0 > 80 {print "High usage on", $6}'`
- Extract a CSV column: `cut -d "," -f2 file.csv`
- Tail a log and filter errors live: `tail -f app.log | grep -i error`

---

## 7. Error Handling and Debugging

**Exit codes**
```bash
ls file.txt
echo $?
# 0 = success, non-zero = error
```
- `exit 0` → success
- `exit 1` → failure
Used to stop a script with a specific status.

**`set -e`** — exits the script immediately if any command fails.

**`set -u`** — treats unset variables as an error:
```bash
set -u
echo "$name"   # fails if $name isn't defined
```

**`set -o pipefail`** — makes a pipeline fail if *any* command in it fails, not just the last one:
```bash
set -o pipefail
grep "error" file.txt | wc -l
```
Without it, only the exit status of the last command (`wc`) is checked.

**`set -x`** — debug mode, traces each command as it executes:
```bash
set -x
echo "Hello"
# + echo Hello
# Hello
```

**`trap`** — runs a cleanup function on exit:
```bash
cleanup() {
    echo "Cleaning up..."
    rm -f temp.txt
}
trap cleanup EXIT

touch temp.txt
# On exit: "Cleaning up..." prints automatically
```

**Putting it all together:**
```bash
#!/bin/bash
set -euo pipefail

cleanup() {
    echo "Cleanup done"
}
trap cleanup EXIT

echo "Running script..."
ls file.txt   # if this fails, script stops immediately
```

---

*** This is the reference shell scripting cheat sheet ***
