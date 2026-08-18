# Day 20 – Bash Scripting Challenge: Log Analyzer and Report Generator

## Task

You are a system administrator responsible for managing a network of servers. Every day, a log file is generated on each server containing important system events and error messages. Your job is to analyze these log files, identify specific events, and generate a summary report.

Write a Bash script (`log_analyzer.sh`) that automates the process of analyzing log files and generating a daily summary report.

---

## Expected Output
- A Bash script: `log_analyzer.sh`
- A generated summary report: `log_report_<date>.txt`
- A markdown file: `day-20-solution.md` documenting your approach

---

## Challenge Tasks

### Task 1: Input and Validation
Your script should:
1. Accept the path to a log file as a command-line argument
2. Exit with a clear error message if no argument is provided
3. Exit with a clear error message if the file doesn't exist

---

### Task 2: Error Count
1. Count the total number of lines containing the keyword `ERROR` or `Failed`
2. Print the total error count to the console

---

### Task 3: Critical Events
1. Search for lines containing the keyword `CRITICAL`
2. Print those lines along with their line number

Example output:
```
--- Critical Events ---
Line 84: 2025-07-29 10:15:23 CRITICAL Disk space below threshold
Line 217: 2025-07-29 14:32:01 CRITICAL Database connection lost
```

---

### Task 4: Top Error Messages
1. Extract all lines containing `ERROR`
2. Identify the **top 5 most common** error messages
3. Display them with their occurrence count, sorted in descending order

Example output:
```
--- Top 5 Error Messages ---
45 Connection timed out
32 File not found
28 Permission denied
15 Disk I/O error
9  Out of memory
```

---

### Task 5: Summary Report
Generate a summary report to a text file named `log_report_<date>.txt` (e.g., `log_report_2026-02-11.txt`). The report should include:
1. Date of analysis
2. Log file name
3. Total lines processed
4. Total error count
5. Top 5 error messages with their occurrence count
6. List of critical events with line numbers

---

## My Approach

`log_analyzer.sh` takes a log file path as its only argument. It validates that the argument was passed and that the file exists, then exits early with a clear message otherwise. It uses `grep -c` for the error/failed count, `grep -n` for critical event extraction with line numbers, and a `grep | sort | uniq -c | sort -nr | head -5` pipeline to get the top 5 error messages. All of this is written to console and also redirected into a dated report file (`log_report_<date>.txt`) using the same values, so the console output and the report stay in sync.

**Script run — console output:**

![log_analyzer output](https://github.com/user-attachments/assets/0c50077b-9e6c-4c04-b7f3-5f146406421a)

**Generated report file:**

![log_report file](https://github.com/user-attachments/assets/1f795b20-4c1c-44ee-a608-ed6d5d7b65d1)

**Script source — `log_analyzer.sh`:**

![log_analyzer.sh script](https://github.com/user-attachments/assets/859570f5-8d1d-4027-95b6-1a18bbac5726)

---

### Task 6 (Optional): Archive Processed Logs
Add a feature to:
1. Create an `archive/` directory if it doesn't exist
2. Move the processed log file into `archive/` after analysis
3. Print a confirmation message

**Implementation:** the script checks for `archive/` with `mkdir -p`, then `mv`s the processed log into it and prints a confirmation line after the report is generated.

![archive feature output](https://github.com/user-attachments/assets/f11aebf4-5c56-4375-8f73-ded3b78a8acc)

![archive directory confirmation](https://github.com/user-attachments/assets/e26855c9-312c-458b-9e1f-c5ebdbf81826)

---

## Key Learnings
- `grep -c` for counting matches, `grep -n` for line-numbered matches
- `sort | uniq -c | sort -nr | head -n` is the standard pipeline for "top N most frequent" problems
- Input validation (`$#` check + `-f` file test) should happen before any processing
- Writing output to both stdout and a file means capturing command output once and reusing it, not running each command twice
