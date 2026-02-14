# Day 21 – Shell Scripting Cheat Sheet: Build Your Own Reference Guide

## 🔹 Quick Reference Table

| Topic | Key Syntax | Example |
|------|-----------|---------|
| Variable | `VAR="value"` | `NAME="DevOps"` |
| Argument | `$1`, `$2` | `./script.sh arg1` |
| If | `if [ condition ]; then` | `if [ -f file ]; then` |
| For loop | `for i in list; do` | `for i in 1 2 3; do` |
| Function | `name() { ... }` | `greet() { echo "Hi"; }` |
| Grep | `grep pattern file` | `grep -i "error" log.txt` |
| Awk | `awk '{print $1}' file` | `awk -F: '{print $1}' /etc/passwd` |
| Sed | `sed 's/old/new/g'` | `sed -i 's/foo/bar/g' file` |

## Task 1: Basics
Document the following with short descriptions and examples:
1. Shebang (`#!/bin/bash`) — what it does and why it matters
2. Running a script — `chmod +x`, `./script.sh`, `bash script.sh`
3. Comments — single line (`#`) and inline
4. Variables — declaring, using, and quoting (`$VAR`, `"$VAR"`, `'$VAR'`)
5. Reading user input — `read`
6. Command-line arguments — `$0`, `$1`, `$#`, `$@`, `$?`

## 🟢 Task 1: Basics

### 1. Shebang
Defines which shell runs the script.
```bash
#!/bin/bash
```
### 2. Running a Script
```bash
chmod +x script.sh
./script.sh
bash script.sh
```
### 3. Comments
```bash
# Single line comment
echo "Hello"  # Inline comment
```
### 4. Variables & Quoting
```bash
VAR="Linux"
echo $VAR
echo "$VAR"   # Expands variable
echo '$VAR'   # Literal
```
### 5. User Input
```bash
read -p "Enter name: " NAME
```
### 6. Command-line Arguments
```bash
$0  # Script name
$1  # First argument
$#  # Argument count
$@  # All arguments
$?  # Last command exit status
```
---

## Task 2: Operators and Conditionals
Document with examples:
1. String comparisons — `=`, `!=`, `-z`, `-n`
2. Integer comparisons — `-eq`, `-ne`, `-lt`, `-gt`, `-le`, `-ge`
3. File test operators — `-f`, `-d`, `-e`, `-r`, `-w`, `-x`, `-s`
4. `if`, `elif`, `else` syntax
5. Logical operators — `&&`, `||`, `!`
6. Case statements — `case ... esac`

## 🟢 Task 2: Operators & Conditionals
### String Comparison
```bash
[ "$a" = "$b" ]
[ "$a" != "$b" ]
[ -z "$var" ]   # Empty
[ -n "$var" ]   # Not empty
```
### Integer Comparison
```bash
[ "$a" -eq 10 ]
[ "$a" -lt 5 ]
[ "$a" -ge 1 ]
```
### File Tests
```bash
[ -f file ]   # Regular file
[ -d dir ]    # Directory
[ -e path ]   # Exists
[ -r file ]   # Readable
[ -w file ]   # Writable
[ -x file ]   # Executable
[ -s file ]   # Not empty
```
### if / elif / else
```bash
if [ condition ]; then
  echo "True"
elif [ other ]; then
  echo "Else if"
else
  echo "False"
fi
```
### Logical Operators
```bash
[ cond1 ] && echo "Yes"
[ cond2 ] || echo "No"
! [ cond ]
```
### Case Statement
```bash
case $1 in
  start) echo "Starting";;
  stop) echo "Stopping";;
  *) echo "Usage: start|stop";;
esac
```
---

## Task 3: Loops
Document with examples:
1. `for` loop — list-based and C-style
2. `while` loop
3. `until` loop
4. Loop control — `break`, `continue`
5. Looping over files — `for file in *.log`
6. Looping over command output — `while read line`

## 🟢 Task 3: Loops
### for Loop (List)
```bash
for i in 1 2 3; do
  echo $i
done
```
### for Loop (C-style)
```bash
for ((i=0; i<5; i++)); do
  echo $i
done
```
### while Loop
```bash
while read line; do
  echo "$line"
done < file.txt
```
### until Loop
```bash
until [ $n -eq 0 ]; do
  echo $n
  ((n--))
done
#break
#continue
```
### Loop Over Files
```bash
for f in *.log; do
  echo "$f"
done
```
---

## Task 4: Functions
Document with examples:
1. Defining a function — `function_name() { ... }`
2. Calling a function
3. Passing arguments to functions — `$1`, `$2` inside functions
4. Return values — `return` vs `echo`
5. Local variables — `local`

## 🟢 Task 4: Functions
### Define & Call
```bash
greet() {
  echo "Hello"
}
greet
```
### Arguments in Functions
```bash
sum() {
  echo $(( $1 + $2 ))
}
sum 2 3
return 0     # Status only
echo "data"  # Output

```
## Local Variable
```bash
myfunc() {
  local x=10
}
```
---

### Task 5: Text Processing Commands
Document the most useful flags/patterns for each:
1. `grep` — search patterns, `-i`, `-r`, `-c`, `-n`, `-v`, `-E`
2. `awk` — print columns, field separator, patterns, `BEGIN/END`
3. `sed` — substitution, delete lines, in-place edit
4. `cut` — extract columns by delimiter
5. `sort` — alphabetical, numerical, reverse, unique
6. `uniq` — deduplicate, count
7. `tr` — translate/delete characters
8. `wc` — line/word/char count
9. `head` / `tail` — first/last N lines, follow mode

# 🟢 Task 5: Text Processing
## grep — search patterns
```bash
grep -i "error" file
grep -r "404" /var/log
grep -c "fail" file
grep -n "root" /etc/passwd
grep -v "info" log
grep -E "error|fail" log
```
### awk — print columns, field separator, patterns, `BEGIN/END`
```bash
awk '{print $1}' file
awk -F: '{print $1}' /etc/passwd
awk 'NR>1 {sum+=$3} END {print sum}' file
```
### sed — substitution, delete lines, in-place edit
```bash
sed 's/old/new/g' file
sed '/error/d' file
sed -i 's/foo/bar/g' file
```
### cut — extract columns by delimiter
```bash
cut -d: -f1 /etc/passwd
```
### sort — alphabetical, numerical, reverse, unique
```bash
sort file
sort -n file
sort -r file
sort -u file
```
### uniq — deduplicate, count
```bash
uniq file
uniq -c file
```
### tr — translate/delete characters
```bash
tr 'a-z' 'A-Z'
tr -d ' '
```
### wc — line/word/char count
```bash
wc -l file
wc -w file
wc -c file
```
### head / tail — first/last N lines, follow mode
```bash
head -5 file
tail -10 file
tail -f app.log
```
---

### Task 6: Useful Patterns and One-Liners
Include at least 5 real-world one-liners you find useful. Examples:
- Find and delete files older than N days
- Count lines in all `.log` files
- Replace a string across multiple files
- Check if a service is running
- Monitor disk usage with alerts
- Parse CSV or JSON from command line
- Tail a log and filter for errors in real time

## 🟢 Task 6: Useful One-Liners
```bash
# Delete files older than 7 days
find /logs -type f -mtime +7 -delete

# Count lines in all .log files
wc -l *.log

# Replace string in multiple files
sed -i 's/dev/prod/g' *.conf

# Check if service is running
systemctl is-active nginx

# Disk usage alert
df -h | awk '$5+0 > 80 {print $0}'

# Tail log & filter errors
tail -f app.log | grep -i error
```

---

### Task 7: Error Handling and Debugging
Document with examples:
1. Exit codes — `$?`, `exit 0`, `exit 1`
2. `set -e` — exit on error
3. `set -u` — treat unset variables as error
4. `set -o pipefail` — catch errors in pipes
5. `set -x` — debug mode (trace execution)
6. Trap — `trap 'cleanup' EXIT`

## 🟢Task 7: Error Handling and Debugging

### 1. Exit Codes
- Every command returns an exit status:
- `0` → Success  
- Non-zero → Failure  

```bash
ls /tmp
echo $?        # Shows exit code of last command

exit 0         # Exit script successfully
exit 1         # Exit script with failure
```
### 2. set -e (Exit on Error) 
- Stops script execution if any command fails.
```bash
set -e

cp file1 file2
rm not_exist_file   # Script exits here
echo "This will not run"
```
### 3. set -u (Unset Variable Error)
- Treats usage of undefined variables as an error.
```bash
set -u

echo "$UNDEFINED_VAR"   # Script exits with error
```
### 4. set -o pipefail (Pipeline Error Handling)
- Fails the pipeline if any command in it fails.
- Without pipefail, only the last command’s status is checked.
```bash
set -o pipefail

cat missing.txt | grep "error"
echo $?    # Returns non-zero if cat fails
```
### 5. set -x (Debug / Trace Mode)
- Prints each command before executing it.
```bash
set -x

echo "Starting script"
ls /tmp
set +x        # Disable debug mode
```
### 6. Trap (Cleanup on Exit)
- Runs a command or function when the script exits.
```bash
cleanup() {
  echo "Cleaning up..."
  rm -f /tmp/tempfile
}

trap cleanup EXIT
```
### Best practice for production scripts:
```bash
set -euo pipefail
-e → exit on error
-u → undefined variables fail
pipefail → pipeline safety
```
---
