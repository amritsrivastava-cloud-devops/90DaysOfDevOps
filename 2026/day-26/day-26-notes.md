# Day 26 – GitHub CLI (gh)

The GitHub CLI (`gh`) allows managing GitHub repositories, issues, pull requests,
and workflows directly from the terminal without switching to the browser.
This is extremely useful for DevOps engineers to automate and script GitHub workflows.

---

## Task 1: Install and Authenticate

### Installation
```bash
sudo apt update
sudo apt install gh -y
```

Authenticate with GitHub
gh auth login

Steps followed:

Selected GitHub.com

Chose HTTPS

Authenticated using browser login

Granted required permissions

Verify Authentication
gh auth status
Authentication Methods Supported by gh

Web-based browser authentication

Personal Access Token (PAT)

SSH key authentication (via Git)

GitHub Enterprise authentication

## Task 2: Working with Repositories
- Create a New Repository
gh repo create gh-cli-test --public --add-readme
- Clone a Repository
gh repo clone <username>/<repo-name>

- View Repository Details
gh repo view
- List All Repositories
gh repo list
- Open Repository in Browser
gh repo view --web
- Delete Repository
gh repo delete <username>/gh-cli-test --confirm

## Task 3: Issues
- Create an Issue
gh issue create \
  --title "Bug: Sample Issue" \
  --body "This issue was created using GitHub CLI" \
  --label bug
  
- List Open Issues
gh issue list
- View a Specific Issue
gh issue view 1
- Close an Issue
gh issue close 1

Automation Use of gh issue
Auto-create issues from monitoring alerts
Close issues automatically after deployments
Generate issue reports using --json output
Integrate with CI/CD pipelines

## Task 4: Pull Requests
- Create Branch, Commit, Push
git checkout -b feature-gh-cli
echo "GitHub CLI PR test" >> test.txt
git add test.txt
git commit -m "Test PR using gh"
git push origin feature-gh-cli

- Create Pull Request
gh pr create --fill
- List Open PRs
gh pr list

- View PR Details
gh pr view

- Merge PR
gh pr merge --merge
Merge Methods Supported

--merge (merge commit)

--squash

--rebase

Reviewing Someone Else’s PR

gh pr checkout <PR-number>

gh pr view <PR-number>

gh pr review --approve

gh pr review --comment

## Task 5: GitHub Actions (Preview)
List Workflow Runs
gh run list --repo owner/repo
View Workflow Run Status
gh run view <run-id>
CI/CD Use Cases

Monitor pipeline failures from terminal

Fetch logs for debugging

Trigger workflows manually

Automate deployment approvals

## Task 6: Useful gh Tricks
Raw GitHub API Calls
gh api repos/<owner>/<repo>
Create a Gist
gh gist create file.txt -d "Sample gist"
Create a Release
gh release create v1.0.0
Create Aliases
gh alias set prc "pr create --fill"
Search Repositories
gh search repos devops
Summary

Using gh, GitHub can be fully managed from the terminal.
This improves productivity, supports automation, and is ideal for DevOps workflows.


---

## Commands 

```
## GitHub CLI (gh) Commands

gh auth login
gh auth status

gh repo create <repo-name> --public --add-readme
gh repo clone <owner>/<repo>
gh repo view
gh repo list
gh repo delete <owner>/<repo> --confirm

gh issue create --title "" --body "" --label ""
gh issue list
gh issue view <issue-number>
gh issue close <issue-number>

gh pr create --fill
gh pr list
gh pr view
gh pr merge --merge|--squash|--rebase
gh pr review --approve

gh run list
gh run view <run-id>

gh api
gh gist create
gh release create
gh alias set
gh search repos

```
