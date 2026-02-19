# Day 25 – Git Reset vs Revert & Branching Strategies

## Challenge Tasks

### Task 1: Git Reset — Hands-On
1. Make 3 commits in your practice repo (commit A, B, C)
2. Use `git reset --soft` to go back one commit — what happens to the changes?
3. Re-commit, then use `git reset --mixed` to go back one commit — what happens now?
4. Re-commit, then use `git reset --hard` to go back one commit — what happens this time?
5. Answer in your notes:
   - What is the difference between `--soft`, `--mixed`, and `--hard`?
   - --soft → moves HEAD only (keeps staged changes)
   - --mixed → moves HEAD + clears staging
   - --hard → moves HEAD + clears staging + deletes changes
     
   - Which one is destructive and why?
   - --hard — because it permanently deletes uncommitted changes.
     
   - When would you use each one?
   - --soft → fix last commit message / regroup commits
   - --mixed → unstage files but keep changes
   - --hard → discard changes completely (⚠️ dangerous)
     
   - Should you ever use `git reset` on commits that are already pushed?
   - No. It rewrites history and breaks shared branches.

```
echo "A" > file.txt
git add file.txt
git commit -m "Commit A"

echo "B" >> file.txt
git commit -am "Commit B"

echo "C" >> file.txt
git commit -am "Commit C"
git reset --soft HEAD~1
git commit -m "Commit C again"
git reset --mixed HEAD~1
git commit -m "Commit C again"
git reset --hard HEAD~1
```
---

### Task 2: Git Revert — Hands-On
1. Make 3 commits (commit X, Y, Z)
2. Revert commit Y (the middle one) — what happens?
3. Check `git log` — is commit Y still in the history?
4. Answer in your notes:
   - How is `git revert` different from `git reset`?
   - Reset vs Revert
   - Reset → rewrites history
   - Revert → adds a new commit that undoes changes
   - Why is revert considered **safer** than reset for shared branches?
   - Because it does not change commit history — safe for shared branches.
   - When would you use revert vs reset?
   - Revert → production / shared branches
   - Reset → local cleanup only

```
echo "X" > revert.txt
git add revert.txt
git commit -m "Commit X"

echo "Y" >> revert.txt
git commit -am "Commit Y"

echo "Z" >> revert.txt
git commit -am "Commit Z"
git revert <commit-hash-of-Y>
git log --oneline
```
---

### Task 3: Reset vs Revert — Summary
Create a comparison in your notes:

|                              | `git reset`         | `git revert`        |
| ---------------------------- | ------------------- | ------------------- |
| What it does                 | Moves HEAD backward | Creates undo commit |
| Removes commit from history? | ✅ Yes               | ❌ No                |
| Safe for pushed branches?    | ❌ No                | ✅ Yes               |
| When to use                  | Local fixes         | Shared / production |


---

### Task 4: Branching Strategies
Research the following branching strategies and document each in your notes with:
1️⃣ GitFlow
- How it works
- main → production
- develop → integration
- feature/*, release/*, hotfix/*
```
Flow

feature → develop → release → main
                     ↘ hotfix ↗
```

- Used in - Enterprise apps , Scheduled releases
- Pros - Clear structure , Good for large teams
- Cons - Heavy & slow , Too complex for startups


2️⃣ GitHub Flow

- How it works
- One main branch
- Short-lived feature branches
- Merge via Pull Requests

```
Flow

main → feature → PR → main
```

- Used in - Web apps , CI/CD environments
- Pros - Simple , Fast delivery
- Cons - Needs strong CI & tests

3️⃣ Trunk-Based Development

- How it works
- Everyone commits to main
- Very short-lived branches (hours)

```
Flow

main ← small commits ← main
```

- Used in - High-velocity teams , Google, Netflix style
- Pros - Fastest feedback , No merge hell
- Cons - Requires discipline , Strong testing mandatory

📝 Strategy Answers

Startup shipping fast?
👉 GitHub Flow / Trunk-Based

Large team, scheduled releases?
👉 GitFlow

Open-source projects mostly use
👉 GitHub Flow

---

## Hints
- `git reflog` is your safety net — it shows everything Git has done, even after a hard reset
- For branching strategies, look at how projects like Kubernetes, React, or Linux kernel manage branches

---
