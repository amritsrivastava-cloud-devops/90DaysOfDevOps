# Day 18 – Shell Scripting: Functions & Slightly Advanced Concepts

## Challenge Tasks

### Task 1: Basic Functions
1. Create `functions.sh` with:
   - A function `greet` that takes a name as argument and prints `Hello, <name>!`
   - A function `add` that takes two numbers and prints their sum
   - Call both functions from the script
     
<img width="802" height="439" alt="image" src="https://github.com/user-attachments/assets/fdb67234-0722-44fe-a936-71cdd902e6ec" />

---

### Task 2: Functions with Return Values
1. Create `disk_check.sh` with:
   - A function `check_disk` that checks disk usage of `/` using `df -h`
   - A function `check_memory` that checks free memory using `free -h`
   - A main section that calls both and prints the results
<img width="937" height="508" alt="image" src="https://github.com/user-attachments/assets/2e1b886e-faed-432f-a29b-a4818d5efecf" />

---

### Task 3: Strict Mode — `set -euo pipefail`
1. Create `strict_demo.sh` with `set -euo pipefail` at the top
2. Try using an **undefined variable** — what happens with `set -u`?
3. Try a command that **fails** — what happens with `set -e`?
4. Try a **piped command** where one part fails — what happens with `set -o pipefail`?

<img width="734" height="307" alt="image" src="https://github.com/user-attachments/assets/5311c873-0d36-445d-9d6f-fab4824dfed3" />
<img width="658" height="68" alt="image" src="https://github.com/user-attachments/assets/2663cf0c-c7da-469f-a29b-b46a47995a31" />
<img width="556" height="69" alt="image" src="https://github.com/user-attachments/assets/60e5df0c-aa18-4e97-bdbe-bf5aad76cf6f" />

**Document:** What does each flag do?
- `set -e` → Script stops immediately when the command fails , Without -e, the script would continue.
- `set -u` → Undefined variable so script exits .
- `set -o pipefail` → It makes a pipeline fail if any command in the pipeline fails.

---

### Task 4: Local Variables
1. Create `local_demo.sh` with:
   - A function that uses `local` keyword for variables
   - Show that `local` variables don't leak outside the function
   - Compare with a function that uses regular variables
<img width="724" height="466" alt="image" src="https://github.com/user-attachments/assets/60cd5b05-29e3-432d-820f-965b591ee4f3" />

---

### Task 5: Build a Script — System Info Reporter
Create `system_info.sh` that uses functions for everything:
1. A function to print **hostname and OS info**
2. A function to print **uptime**
3. A function to print **disk usage** (top 5 by size)
4. A function to print **memory usage**
5. A function to print **top 5 CPU-consuming processes**
6. A `main` function that calls all of the above with section headers
7. Use `set -euo pipefail` at the top

Output should look clean and readable.
<img width="1160" height="519" alt="image" src="https://github.com/user-attachments/assets/884dec00-bc2d-46c7-ab32-660286b1f225" />
<img width="1143" height="662" alt="image" src="https://github.com/user-attachments/assets/e4b980d7-79cf-4d2f-99fa-7419656b8c69" />


---

## Hints
- Function syntax: `function_name() { ... }`
- Local vars: `local MY_VAR="value"`
- Strict mode: `set -euo pipefail` as first line after shebang
- Pass args to functions: `greet "Shubham"` → access as `$1` inside
- `$?` gives the exit code of last command

---
