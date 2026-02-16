# Git Commands Cheat Sheet

## Installation & Setup

| Category | Command | Description |
|--------|---------|-------------|
| Install | `sudo apt install git` | Install Git on system |
| Version | `git --version` | Check installed Git version |
| Config | `git config --global user.name "amritsrivastava-cloud-devops"` | Set global username |
| Config | `git config --global user.email "amrits.cloud@gmail.com"` | Set global email |

---

## Repository Basics

| Category | Command | Description |
|--------|---------|-------------|
| Repo | `git init` | Initialize a new Git repository |
| Status | `git status` | Show working tree status |
| Stage | `git add <file>` | Move file from untracked to staged |
| Unstage | `git rm --cached <file>` | Move file from staged to untracked |
| Restore | `git restore <file>` | Discard local changes |
| Commit | `git commit -m "message"` | Save changes to repository |
| History | `git log` | Show commit hash, author, email |

---

## Branching

| Category | Command | Description |
|--------|---------|-------------|
| Branch | `git branch` | List all local branches |
| Branch | `git branch <branch-name>` | Create a new branch |
| Switch | `git checkout <branch-name>` | Switch branch (legacy) |
| Switch | `git checkout -b <branch-name>` | Create & switch branch |
| Switch | `git switch <branch-name>` | Switch branch (modern) |
| Switch | `git switch -c <branch-name>` | Create & switch branch (modern) |
| Delete | `git branch -D <branch-name>` | Force delete branch |

---

## Remote Repositories

| Category | Command | Description |
|--------|---------|-------------|
| Remote | `git remote add origin <repo-url>` | Add remote repository |
| Remote | `git remote -v` | Show remote URLs |
| Clone | `git clone <repo-url>` | Clone a repository |
| Push | `git push origin main` | Push local main branch |
| Pull | `git pull origin main` | Fetch and merge changes |
| Push | `git push -u origin main` | Push and set upstream |

---

## Fork & Upstream Sync

| Category | Command | Description |
|--------|---------|-------------|
| Upstream | `git remote add upstream <repo-url>` | Add original repo |
| Fetch | `git fetch upstream` | Fetch upstream changes |
| Branch | `git branch -a` | List local & remote branches |
| Merge | `git merge upstream/main` | Merge upstream into local main |

---
