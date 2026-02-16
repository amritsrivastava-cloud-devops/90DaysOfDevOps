# Day 23 – Git Branching & Working with GitHub

## Task

Now that you know how to create repos, stage, and commit — it's time to learn the most powerful concept in Git: **branching**.
Branches let you work on features, fixes, and experiments in isolation without breaking your main code.
You'll also push your work to GitHub for the first time.

---

## Challenge Tasks

### Task 1: Understanding Branches

#### 1. What is a branch in Git?
A branch in Git is a lightweight pointer to a commit. It allows you to work on changes independently without affecting other branches like main.

#### 2. Why do we use branches instead of committing everything to main?
Branches allow:
Safe feature development
Bug fixes without breaking production code
Parallel work by multiple developers
Easy testing and rollback
Keeping main clean and stable is the goal.

#### 3. What is HEAD in Git?
HEAD is a pointer that shows your current working branch and commit. When you switch branches, HEAD moves to point to the new branch.

#### 4. What happens to your files when you switch branches?
Git updates your working directory to match the snapshot of the branch you switch to. Files may change, appear, or disappear depending on that branch’s commits.

---

### Task 2: Branching Commands — Hands-On
In your `devops-git-practice` repo, perform the following:
1. List all branches in your repo
2. Create a new branch called `feature-1`
3. Switch to `feature-1`
4. Create a new branch and switch to it in a single command — call it `feature-2`
5. Try using `git switch` to move between branches — how is it different from `git checkout`?
6. Make a commit on `feature-1` that does **not** exist on `main`
7. Switch back to `main` — verify that the commit from `feature-1` is not there
8. Delete a branch you no longer need
9. Add all branching commands to your `git-commands.md`

```bash
git branch
git branch branch-name
git checkout branch-name
git checkout -b branch-name
git switch branch-name
git switch -c branch-name
git branch -d branch-name
```
<img width="1354" height="897" alt="image" src="https://github.com/user-attachments/assets/279e013b-6fc5-4628-a726-1fd1da757f65" />

---

### Task 3: Push to GitHub
1. Create a **new repository** on GitHub (do NOT initialize it with a README)
2. Connect your local `devops-git-practice` repo to the GitHub remote
3. Push your `main` branch to GitHub
4. Push `feature-1` branch to GitHub
5. Verify both branches are visible on GitHub
6. Answer in your notes: What is the difference between `origin` and `upstream`?

<img width="943" height="861" alt="image" src="https://github.com/user-attachments/assets/28e44a74-1453-4475-937e-4fbea00d15a2" />
<img width="949" height="651" alt="image" src="https://github.com/user-attachments/assets/fbfe05ba-2fcb-4034-b99b-c6d38cee06f1" />
<img width="944" height="750" alt="image" src="https://github.com/user-attachments/assets/25d1aa99-e12f-4a2d-8954-327047643785" />

```
origin → your fork or primary remote repo
upstream → original repository (used mostly after forking)
```

---

### Task 4: Pull from GitHub
1. Make a change to a file **directly on GitHub** (use the GitHub editor)
2. Pull that change to your local repo
3. Answer in your notes: What is the difference between `git fetch` and `git pull`?

<img width="942" height="575" alt="image" src="https://github.com/user-attachments/assets/b3c4fc05-49dc-44be-a648-a69bdf388066" />
<img width="817" height="482" alt="image" src="https://github.com/user-attachments/assets/c24ed530-c306-4f32-915e-626f79f19965" />

```
git fetch → downloads changes without merging
git pull → fetch + merge in one step
```
---

### Task 5: Clone vs Fork
1. **Clone** any public repository from GitHub to your local machine
<img width="807" height="305" alt="image" src="https://github.com/user-attachments/assets/f89d5463-1ac4-447d-888c-b7e954967226" />

2. **Fork** the same repository on GitHub, then clone your fork
<img width="944" height="551" alt="image" src="https://github.com/user-attachments/assets/127312f6-7eac-4ca2-86e2-9f8821fb735e" />

3. Answer in your notes:
   - What is the difference between clone and fork?
   - Clone
   - Local copy of a repo
   - No ownership
   - Used for learning or contributing with access
   
   - Fork
   - Your own copy on GitHub
   - Full control
   - Used to contribute to open-source projects
     
   - When would you clone vs fork?
   - Clone → personal work, internal repos
   - Fork → open-source contributions
     
   - After forking, how do you keep your fork in sync with the original repo?
   - 
   <img width="947" height="445" alt="image" src="https://github.com/user-attachments/assets/b5541747-1675-4d20-8398-894fe3f25b12" />
   <img width="846" height="126" alt="image" src="https://github.com/user-attachments/assets/a0fca262-2618-4498-a9c4-c858d0d78356" />
   
```
Original Repo (upstream)
        ↓ fetch
Local Repo (main)
        ↓ push
Your Fork (origin)
```
---

## Hints
- When you create a branch, it starts from the commit you're currently on
- `git switch` is the modern alternative to `git checkout` for switching branches
- To push a new branch: `git push -u origin <branch-name>`
- A fork is a GitHub concept, not a Git concept
