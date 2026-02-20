# Day 24 – Advanced Git: Merge, Rebase, Stash & Cherry Pick

## Challenge Tasks

### Task 1: Git Merge — Hands-On
1. Create a new branch `feature-login` from `main`, add a couple of commits to it
2. Switch back to `main` and merge `feature-login` into `main`
3. Observe the merge — did Git do a **fast-forward** merge or a **merge commit**?
4. Now create another branch `feature-signup`, add commits to it — but also add a commit to `main` before merging
5. Merge `feature-signup` into `main` — what happens this time?
6. Answer in your notes:
   - What is a fast-forward merge?
   - A fast-forward merge happens when the target branch has no new commits. Git just moves the branch pointer forward.
     
   - When does Git create a merge commit instead?
   - When both branches have diverged (both have new commits).
     
   - What is a merge conflict? (try creating one intentionally by editing the same line in both branches)
   - When the same line of a file is changed differently in two branches and Git can’t auto-merge.
   - To create a conflict: edit the same line in the same file on both branches and merge.

```
commmands:-
## Create Feature login and adding commit 
git checkout -b feature-login
echo "Login pace i am creating " > login_page.txt
git add login_page.txt
git commit -m "Add login page into project "

echo "Login validation added" >> login_page.txt
git commit -am "Add login validation"
git checkout main
git merge feature-login
git log --oneline --graph
git checkout -b feature-signup
echo "Signup page" > signup.txt
git add signup.txt
git commit -m "Add signup page"

git checkout main
echo "Hotfix in main" > hotfix.txt
git add hotfix.txt
git commit -m "Hotfix on main"
git merge feature-signup
```

<img width="2238" height="1278" alt="image" src="https://github.com/user-attachments/assets/49811f35-ad23-41b6-a25e-9ca30c494e74" />
<img width="2066" height="1460" alt="image" src="https://github.com/user-attachments/assets/406baeed-0d87-4a11-96a7-e7f4f1aaba10" />

---

### Task 2: Git Rebase — Hands-On
1. Create a branch `feature-dashboard` from `main`, add 2-3 commits
2. While on `main`, add a new commit (so `main` moves ahead)
3. Switch to `feature-dashboard` and rebase it onto `main`
4. Observe your `git log --oneline --graph --all` — how does the history look compared to a merge?
5. Answer in your notes:
   - What does rebase actually do to your commits?
   - Rebase replays your commits on top of another branch, rewriting commit history.
     
   - How is the history different from a merge?
   - Merge → branching history
   - Rebase → clean, straight-line history
     
   - Why should you **never rebase commits that have been pushed and shared** with others?
   - Because rebase rewrites commit hashes, breaking other developers’ history.
     
   - When would you use rebase vs merge?
   - Rebase → clean up local feature branches
   - Merge → integrate shared work safely

```bash
git checkout -b feature-dashboard
echo "Dashboard v1" > dashboard.txt
git add dashboard.txt
git commit -m "Add dashboard"

echo "Dashboard charts" >> dashboard.txt
git commit -am "Add charts"
git checkout main
echo "Main update" > main.txt
git add main.txt
git commit -m "Update main"
git checkout feature-dashboard
git rebase main
git log --oneline --graph --all
```
---

### Task 3: Squash Commit vs Merge Commit
1. Create a branch `feature-profile`, add 4-5 small commits (typo fix, formatting, etc.)
2. Merge it into `main` using `--squash` — what happens?
3. Check `git log` — how many commits were added to `main`?
4. Now create another branch `feature-settings`, add a few commits
5. Merge it into `main` **without** `--squash` (regular merge) — compare the history
6. Answer in your notes:
   - What does squash merging do?
   - Combines all feature branch commits into one commit on main.
     
   - When would you use squash merge vs regular merge?
   - For small features, typo fixes, cleanup commits.
     
   - What is the trade-off of squashing?
   - Loses detailed commit history.

```
git checkout -b feature-profile
echo "Profile page" > profile.txt
git add profile.txt
git commit -m "Add profile page"

echo "Fix typo" >> profile.txt
git commit -am "Fix typo"

echo "Format text" >> profile.txt
git commit -am "Format profile"
git checkout main
git merge --squash feature-profile
git commit -m "Add profile feature"
git log --oneline
git checkout -b feature-settings
echo "Settings page" > settings.txt
git add settings.txt
git commit -m "Add settings"

git checkout main
git merge feature-settings
```
---

### Task 4: Git Stash — Hands-On
1. Start making changes to a file but **do not commit**
2. Now imagine you need to urgently switch to another branch — try switching. What happens?
3. Use `git stash` to save your work-in-progress
4. Switch to another branch, do some work, switch back
5. Apply your stashed changes using `git stash pop`
6. Try stashing multiple times and list all stashes
7. Try applying a specific stash from the list
8. Answer in your notes:
   - What is the difference between `git stash pop` and `git stash apply`?
   - pop → applies + deletes stash
   - apply → applies but keeps stash
     
   - When would you use stash in a real-world workflow?
   - When switching context quickly without committing unfinished work.

```
echo "WIP change" >> login.txt
git checkout feature-login
git stash
git checkout main
git checkout feature-login
git stash pop
git stash
git stash
git stash list
git stash apply stash@{1}

```
---

### Task 5: Cherry Picking
1. Create a branch `feature-hotfix`, make 3 commits with different changes
2. Switch to `main`
3. Cherry-pick **only the second commit** from `feature-hotfix` onto `main`
4. Verify with `git log` that only that one commit was applied
5. Answer in your notes:
   - What does cherry-pick do?
   - Applies a specific commit from another branch.
     
   - When would you use cherry-pick in a real project?
   - For hotfixes or selective bug fixes.
     
   - What can go wrong with cherry-picking?
   - Conflicts
   - Duplicate commits
   - Broken context if dependencies are missing

```
git checkout -b feature-hotfix
echo "Fix A" > fix.txt
git add fix.txt
git commit -m "Fix A"

echo "Fix B" >> fix.txt
git commit -am "Fix B"

echo "Fix C" >> fix.txt
git commit -am "Fix C"
git checkout main
git cherry-pick <commit-hash-of-Fix-B>
git log --oneline
```
---

## Hints
- Visualize history: `git log --oneline --graph --all`
- To intentionally create a merge conflict: edit the **same line** of the **same file** on two branches
- Stash with a message: `git stash push -m "description"`
- Cherry-pick needs a commit hash — find it with `git log --oneline`
