# Day 06 – Linux Fundamentals: Read and Write Text Files

**Goal:** Practice basic file read, write, and append commands.

## Commands & Output

| Command | Action |
|---|---|
| `touch notes.txt` | Creates an empty file |
| `echo "Learning Linux" > notes.txt` | Writes first line (overwrites file) |
| `echo "Practicing file commands" >> notes.txt` | Appends second line |
| `echo "DevOps journey Day 06" \| tee -a notes.txt` | Appends *and* prints to terminal (`-a` = append, `tee` writes + displays simultaneously) |

**Resulting `notes.txt`:**
```
Learning Linux
Practicing file commands
DevOps journey Day 06
```

## Reading Parts of a File

**`head -n 2 notes.txt`** — prints the first 2 lines
```
Learning Linux
Practicing file commands
```

**`tail -n 2 notes.txt`** — prints the last 2 lines
```
Practicing file commands
DevOps journey Day 06
```

Output Screenshot : <img width="850" height="356" alt="image" src="https://github.com/user-attachments/assets/dd7935ea-2edb-477c-9c19-cb6740e16379" />

