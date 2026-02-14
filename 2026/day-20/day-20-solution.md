# Day 20 – Bash Scripting Challenge: Log Analyzer and Report Generator

## Task
- You are a system administrator responsible for managing a network of servers. Every day, a log file is generated on each server containing important system events and error messages. Your job is to analyze these log files, identify specific events, and generate a summary report.
- Write a Bash script (`log_analyzer.sh`) that automates the process of analyzing log files and generating a daily summary report.
## Challenge Tasks

### Task 1: Input and Validation
Your script should:
1. Accept the path to a log file as a command-line argument
2. Exit with a clear error message if no argument is provided
3. Exit with a clear error message if the file doesn't exist

### Task 2: Error Count
1. Count the total number of lines containing the keyword `ERROR` or `Failed`
2. Print the total error count to the console

### Task 3: Critical Events
1. Search for lines containing the keyword `CRITICAL`
2. Print those lines along with their line number

Example output:
```
--- Critical Events ---
Line 84: 2025-07-29 10:15:23 CRITICAL Disk space below threshold
Line 217: 2025-07-29 14:32:01 CRITICAL Database connection lost
```
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
### Task 5: Summary Report
Generate a summary report to a text file named `log_report_<date>.txt` (e.g., `log_report_2026-02-11.txt`). The report should include:
1. Date of analysis
2. Log file name
3. Total lines processed
4. Total error count
5. Top 5 error messages with their occurrence count
6. List of critical events with line numbers

### Task 6 (Optional): Archive Processed Logs
Add a feature to:
1. Create an `archive/` directory if it doesn't exist
2. Move the processed log file into `archive/` after analysis
3. Print a confirmation message

## Sample Log File
- A sample log file is available in this directory: `sample_log.log`
- You can also pick real-world log datasets from the [LogHub repository](https://github.com/logpai/loghub) to test your script against production-like logs (e.g., ZooKeeper, HDFS, Apache, Linux syslogs).

## Hints
- Count errors: `grep -c "ERROR" logfile.log`
- Print with line numbers: `grep -n "CRITICAL" logfile.log`
- Top occurrences: `grep "ERROR" logfile.log | awk '{$1=$2=$3=""; print}' | sort | uniq -c | sort -rn | head -5`
- Associative arrays: `declare -A error_map`
- Date for filename: `date +%Y-%m-%d`
- Move files: `mv logfile.log archive/`

## Output 
-
<img width="962" height="198" alt="image" src="https://github.com/user-attachments/assets/2e83a051-0403-4b54-8de3-af4b67bb3eeb" />
<img width="1292" height="777" alt="image" src="https://github.com/user-attachments/assets/de097fc7-17bf-4a03-8d46-8a26025c97bd" />
<img width="851" height="552" alt="image" src="https://github.com/user-attachments/assets/e8760b76-42bf-4617-b130-4869f2b57296" />

---

```bash
#!/bin/bash
set -euo pipefail

#Task 1: Input & Validation

# Check if log file argument is provided
if [ "$#" -ne 1 ]; then
    echo "Usage: $0 <log_file_path>"
    exit 1
fi

LOG_FILE="$1"

# Check if file exists
if [ ! -f "$LOG_FILE" ]; then
    echo "Error: Log file '$LOG_FILE' does not exist."
    exit 1
fi

#Defining Variables

DATE=$(date +%Y-%m-%d)
REPORT_FILE="log_report_${DATE}.txt"
TOTAL_LINES=$(wc -l < "$LOG_FILE")

echo "Analyzing log file: $LOG_FILE"
echo "-----------------------------------"


#Task 2: Error Count

ERROR_COUNT=$(grep -Ei "ERROR|Failed" "$LOG_FILE" | wc -l)

echo "Total Errors (ERROR or Failed): $ERROR_COUNT"

#Task 3: Critical Events

CRITICAL_EVENTS=$(grep -n "CRITICAL" "$LOG_FILE" || true)

echo
echo "--- Critical Events ---"
if [ -z "$CRITICAL_EVENTS" ]; then
    echo "No CRITICAL events found."
else
    echo "$CRITICAL_EVENTS"
fi


#Task 4: Top 5 Error Messages

TOP_ERRORS=$(grep "ERROR" "$LOG_FILE" \
    | awk '{$1=$2=$3=""; print}' \
    | sort \
    | uniq -c \
    | sort -rn \
    | head -5 || true)

echo
echo "--- Top 5 Error Messages ---"
if [ -z "$TOP_ERRORS" ]; then
    echo "No ERROR messages found."
else
    echo "$TOP_ERRORS"
fi

#Task 5: Summary Report

{
    echo "Log Analysis Report"
    echo "==================="
    echo "Date: $DATE"
    echo "Log File: $LOG_FILE"
    echo "Total Lines Processed: $TOTAL_LINES"
    echo "Total Errors: $ERROR_COUNT"
    echo
    echo "--- Top 5 Error Messages ---"
    if [ -z "$TOP_ERRORS" ]; then
        echo "No ERROR messages found."
    else
        echo "$TOP_ERRORS"
    fi
    echo
    echo "--- Critical Events ---"
    if [ -z "$CRITICAL_EVENTS" ]; then
        echo "No CRITICAL events found."
    else
        echo "$CRITICAL_EVENTS"
    fi
} > "$REPORT_FILE"

echo
echo "Summary report generated: $REPORT_FILE"


#Task 6 (Optional): Archive Logs

ARCHIVE_DIR="archive"

if [ ! -d "$ARCHIVE_DIR" ]; then
    mkdir "$ARCHIVE_DIR"
fi

mv "$LOG_FILE" "$ARCHIVE_DIR/"

echo "Log file archived to $ARCHIVE_DIR/"
