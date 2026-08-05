# Day 10 -- Linux File Permissions & File Operations

## Objective

Practice creating, reading, and managing files while learning Linux file
permissions using `chmod`.

## Tasks

### Task 1 -- Create Files

-   Create `devops.txt` using `touch`
-   Create `notes.txt` using `echo` or `cat`
-   Create `script.sh` using `vim` with:

``` bash
echo "Hello DevOps"
```

-   Verify with:

``` bash
ls -l
```

### Task 2 -- Read Files

-   Read `notes.txt` using `cat`
-   Open `script.sh` in read-only mode using `vim -R`
-   Display the first 5 lines of `/etc/passwd` using `head`
-   Display the last 5 lines using `tail`

**Verification:** Screenshot attached in the original submission.

### Task 3 -- Understand Permissions

Permission format:

``` text
rwxrwxrwx
```

-   Owner \| Group \| Others
-   `r = 4`, `w = 2`, `x = 1`

Check permissions:

``` bash
ls -l devops.txt notes.txt script.sh
```

### Task 4 -- Modify Permissions

-   Make `script.sh` executable
-   Make `devops.txt` read-only
-   Set `notes.txt` permission to `640`
-   Create `project/` with permission `755`
-   Verify each change using `ls -l`

### Task 5 -- Test Permissions

-   Try writing to a read-only file
-   Try executing a file without execute permission
-   Observe and document the error messages

## chmod Reference

`chmod a-w script.sh`

-   `a` → All (`u + g + o`)
-   `u` → User (Owner)
-   `g` → Group
-   `o` → Others

Permission symbols: - `r` → Read - `w` → Write - `x` → Execute

## Summary

### Files Created

-   `devops.txt`
-   `notes.txt`
-   `script.sh`

### Permission Changes

-   `script.sh` → Executable
-   `devops.txt` → Read-only
-   `notes.txt` → Permission `640`
-   `project/` → Permission `755`

### Commands Practiced

`touch`, `echo`, `cat`, `vim`, `head`, `tail`, `ls`, `chmod`

### Key Learnings

-   Linux permission structure (`rwx`)
-   Numeric and symbolic permissions
-   Using `chmod` to control file access
-   How permissions affect reading, writing, and execution
