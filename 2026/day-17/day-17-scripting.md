# Day 17 – Shell Scripting: Loops, Arguments & Error Handling

## Challenge Tasks

### Task 1: For Loop
1. Create `for_loop.sh` that:
   - Loops through a list of 5 fruits and prints each one
<img width="1300" height="512" alt="image" src="https://github.com/user-attachments/assets/eea54225-293b-4124-9cdd-beb5c8593f17" />


2. Create `count.sh` that:
   - Prints numbers 1 to 10 using a for loop
<img width="1206" height="788" alt="image" src="https://github.com/user-attachments/assets/0f48d883-85d7-4359-bc96-496304b4a657" />

---

### Task 2: While Loop
1. Create `countdown.sh` that:
   - Takes a number from the user
   - Counts down to 0 using a while loop
   - Prints "Done!" at the end
<img width="1424" height="832" alt="image" src="https://github.com/user-attachments/assets/e333ce08-76f9-4e51-8061-bbdbeab7aa91" />

---

### Task 3: Command-Line Arguments
1. Create `greet.sh` that:
   - Accepts a name as `$1`
   - Prints `Hello, <name>!`
   - If no argument is passed, prints "Usage: ./greet.sh <name>"
<img width="1176" height="518" alt="image" src="https://github.com/user-attachments/assets/0b1d58c1-dae9-45c4-8ea9-227293a612d3" />

2. Create `args_demo.sh` that:
   - Prints total number of arguments (`$#`)
   - Prints all arguments (`$@`)
   - Prints the script name (`$0`)
<img width="1862" height="700" alt="image" src="https://github.com/user-attachments/assets/aa26770e-4d6f-4868-b59f-26932476105d" />


---

### Task 4: Install Packages via Script
1. Create `install_packages.sh` that:
   - Defines a list of packages: `nginx`, `curl`, `wget`
   - Loops through the list
   - Checks if each package is installed (use `dpkg -s` or `rpm -q`)
   - Installs it if missing, skips if already present
   - Prints status for each package

> Run as root: `sudo -i` or `sudo su`

---

### Task 5: Error Handling
1. Create `safe_script.sh` that:
   - Uses `set -e` at the top (exit on error)
   - Tries to create a directory `/tmp/devops-test`
   - Tries to navigate into it
   - Creates a file inside
   - Uses `||` operator to print an error if any step fails
<img width="2890" height="620" alt="image" src="https://github.com/user-attachments/assets/78b4d2dd-5596-4760-87e9-6c4d35472b48" />
<img width="1352" height="480" alt="image" src="https://github.com/user-attachments/assets/daabc86d-3c03-4aa3-afc3-fba03706327f" />


Example:
```bash
mkdir /tmp/devops-test || echo "Directory already exists"
```

2. Modify your `install_packages.sh` to check if the script is being run as root — exit with a message if not.

---

## Hints
- For loop: `for item in list; do ... done`
- While loop: `while [ condition ]; do ... done`
- Arguments: `$1` first arg, `$#` count, `$@` all args
- Check root: `if [ "$EUID" -ne 0 ]; then echo "Run as root"; exit 1; fi`
- Check package: `dpkg -s <pkg> &> /dev/null && echo "installed"`

---
