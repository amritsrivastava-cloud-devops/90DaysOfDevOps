# Day 22 – Introduction to Git: Your First Repository

### Task 1: Install and Configure Git
1. Verify Git is installed on your machine
2. Set up your Git identity — name and email
3. Verify your configuration

```bash
sudo apt install git
git --version
git config --global user.name amritsrivastava-cloud-devops
git config --global user.email amrits.cloud@gmail.com
```

<img width="1241" height="667" alt="image" src="https://github.com/user-attachments/assets/6f81d4b3-5132-4e12-8f70-76a57037f13f" />

---

### Task 2: Create Your Git Project
1. Create a new folder called `devops-git-practice`
2. Initialize it as a Git repository
3. Check the status — read and understand what Git is telling you
4. Explore the hidden `.git/` directory — look at what's inside

```bash
git init
git status
```

<img width="1202" height="622" alt="image" src="https://github.com/user-attachments/assets/95bbf14c-3d00-4df6-a7a0-40dc9652dcf8" />
<img width="1246" height="357" alt="image" src="https://github.com/user-attachments/assets/6d1faac9-4540-4d09-885f-ebb3eadbfe53" />

---

### Task 3: Create Your Git Commands Reference

```bash
sudo apt install git   
git --version
git init (initialize git repo)
git add (add from untraced to staged)
git rm --cached filename (move from staged to untraced)
git commit -m "messge" (commited once can't removed permanently , will be recovered if deleted)
git log (shows hash username email )
git status (check status untracked, staged , tracked )
git restore filename (if deleted from staging )
git config --global user.name amritsrivastava-cloud-devops
git config --global user.email amrits.cloud@gmail.com
git checkout -b dev (create a new branch and copy all info of master)
git branch (list all branch )
git branch -D dev (delete branch )
git checkout dev (switch branch)
git switch dev (switch branch)
```
---

### Task 4: Stage and Commit
1. Stage your file
2. Check what's staged
3. Commit with a meaningful message
4. View your commit history
<img width="1409" height="987" alt="image" src="https://github.com/user-attachments/assets/0982683b-9e39-4984-9182-0da7d3c30cb8" />

---

### Task 5: Make More Changes and Build History
1. Edit `git-commands.md` — add more commands as you discover them
2. Check what changed since your last commit
3. Stage and commit again with a different, descriptive message
4. Repeat this process at least **3 times** so you have multiple commits in your history
5. View the full history in a compact format
<img width="1659" height="908" alt="image" src="https://github.com/user-attachments/assets/6d26b346-46e8-413b-a454-1672d5883e2e" />
<img width="1063" height="385" alt="image" src="https://github.com/user-attachments/assets/40fbd701-f30a-44b8-93c5-194d5aff3a3c" />

---

### Task 6: Understand the Git Workflow

#### 1. Difference between git add and git commit

```bash
git add moves changes from the working directory to the staging area.
It tells Git “I want to include these changes in the next commit.”
git commit saves the staged changes permanently into the repository with a message.
It tells Git “Finalize and record these changes.”
👉 In short:
git add = prepare changes
git commit = save changes
```
#### 2. What does the staging area do? Why doesn’t Git commit directly?
```bash
The staging area acts as a preview layer between editing files and committing them.
It allows you to:
Select specific files or parts of files to commit
Review what will go into the commit
Create clean, logical commits instead of dumping everything at once
If Git committed directly:
You’d have no control over what goes into a commit
Commits would be messy and harder to track or revert

👉 Staging = control + clarity
```
#### 3. What information does git log show?
```
git log shows the commit history, including:
Commit hash (unique ID)
Author name and email
Date and time of commit
Commit message

This helps you track:
What changes were made
Who made them
When they were made
<img width="1131" height="532" alt="image" src="https://github.com/user-attachments/assets/99004536-ffb0-48bf-9214-9940cb26eec4" />

```
#### 4. What is the .git/ folder? What happens if you delete it?
```
The .git/ folder is the heart of the Git repository.
It contains:
Commit history
Branch information
Configuration
Staging data
<img width="1044" height="146" alt="image" src="https://github.com/user-attachments/assets/22162a2c-2691-4d80-8473-cd6bf0aeb268" />

If you delete the .git/ folder:
The project is no longer a Git repository
All version history is lost
Files remain, but Git tracking is gone

👉 Deleting .git/ = deleting Git itself for that project
```
#### 5. Difference between working directory, staging area, and repository
```
Working Directory
Where you edit files (actual project files on disk)

Staging Area
A temporary area that holds changes you’ve marked for commit (git add)

Repository
The permanent history of commits stored by Git (git commit)

👉 Flow:

Working Directory → Staging Area → Repository

```
---
## Hints
- All you need today are about 8-10 Git commands — Google them, try them, break things
- Read what `git status` tells you — it's your best friend
- Use `man git-<command>` or `git <command> --help` to explore
