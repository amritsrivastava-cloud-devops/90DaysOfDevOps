# Day 16 – Shell Scripting Basics

## Challenge Tasks

### Task 1: Your First Script
1. Create a file `hello.sh`
2. Add the shebang line `#!/bin/bash` at the top
3. Print `Hello, DevOps!` using `echo`
4. Make it executable and run it

```bash
chmod +x hello.sh
./hello.sh
```
<img width="768" height="327" alt="image" src="https://github.com/user-attachments/assets/9a66f630-b6bc-4aa4-a533-609563b62a78" />
<img width="632" height="311" alt="image" src="https://github.com/user-attachments/assets/96e3c1c4-ea0d-4178-87db-c277f779db0a" />

**Document:** What happens if you remove the shebang line?
- no change 
---

### Task 2: Variables
1. Create `variables.sh` with:
   - A variable for your `NAME`
   - A variable for your `ROLE` (e.g., "DevOps Engineer")
   - Print: `Hello, I am <NAME> and I am a <ROLE>`

<img width="774" height="335" alt="image" src="https://github.com/user-attachments/assets/7c822832-ed44-4cbe-85b6-9787e4257786" />
<img width="788" height="169" alt="image" src="https://github.com/user-attachments/assets/7b3e63a5-b63a-4621-b582-17b162804e88" />

2. Try using single quotes vs double quotes — what's the difference?
- no difference "
---

### Task 3: User Input with read
1. Create `greet.sh` that:
   - Asks the user for their name using `read`
   - Asks for their favourite tool
   - Prints: `Hello <name>, your favourite tool is <tool>`

<img width="766" height="278" alt="image" src="https://github.com/user-attachments/assets/015a6b89-476f-4a50-b9ee-6101ea9c8e7c" />
<img width="690" height="314" alt="image" src="https://github.com/user-attachments/assets/5dea0c92-8aa0-4a05-a841-ef9c2c3240ea" />

---

### Task 4: If-Else Conditions
1. Create `check_number.sh` that:
   - Takes a number using `read`
   - Prints whether it is **positive**, **negative**, or **zero**
<img width="771" height="356" alt="image" src="https://github.com/user-attachments/assets/b865f673-c4fa-4173-a76b-9703e98c0469" />
<img width="748" height="255" alt="image" src="https://github.com/user-attachments/assets/88eb5f99-fe0b-4ffa-997a-bd80c0ee7515" />


2. Create `file_check.sh` that:
   - Asks for a filename
   - Checks if the file **exists** using `-f`
   - Prints appropriate message
<img width="802" height="179" alt="image" src="https://github.com/user-attachments/assets/6193a32b-7213-4765-8254-9b6e8c6a8a99" />
<img width="781" height="322" alt="image" src="https://github.com/user-attachments/assets/4c7ea373-40eb-42d4-973d-4fa1f323b62e" />

---

### Task 5: Combine It All
Create `server_check.sh` that:
1. Stores a service name in a variable (e.g., `nginx`, `sshd`)
2. Asks the user: "Do you want to check the status? (y/n)"
3. If `y` — runs `systemctl status <service>` and prints whether it's **active** or **not**
4. If `n` — prints "Skipped."

---

## Hints
- Shebang: `#!/bin/bash` tells the system which interpreter to use
- Variables: `NAME="Shubham"` (no spaces around `=`)
- Read: `read -p "Enter name: " NAME`
- If syntax: `if [ condition ]; then ... elif ... else ... fi`
- File check: `if [ -f filename ]; then`


- What you learned (3 key points)
