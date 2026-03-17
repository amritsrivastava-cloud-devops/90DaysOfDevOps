# Day 47 – Advanced Triggers: PR Events, Cron Schedules & Event-Driven Pipelines

## Challenge Tasks

### Task 1: Pull Request Event Types
Create `.github/workflows/pr-lifecycle.yml` that triggers on `pull_request` with **specific activity types**:
1. Trigger on: `opened`, `synchronize`, `reopened`, `closed`
2. Add steps that:
   - Print which event type fired: `${{ github.event.action }}`
   - Print the PR title: `${{ github.event.pull_request.title }}`
   - Print the PR author: `${{ github.event.pull_request.user.login }}`
   - Print the source branch and target branch
3. Add a conditional step that only runs when the PR is **merged** (closed + merged = true)

Test it: create a PR, push an update to it, then merge it. Watch the workflow fire each time with a different event type.

```
name: PR Lifecycle Events

on:
  pull_request:
    types: [opened, synchronize, reopened, closed]

jobs:
  pr-info:
    runs-on: ubuntu-latest

    steps:
      - name: Print PR details
        run: |
          echo "Event Type: ${{ github.event.action }}"
          echo "PR Title: ${{ github.event.pull_request.title }}"
          echo "PR Author: ${{ github.event.pull_request.user.login }}"
          echo "Source Branch: ${{ github.head_ref }}"
          echo "Target Branch: ${{ github.base_ref }}"

      - name: Run only if PR merged
        if: github.event.pull_request.merged == true
        run: echo "PR was merged successfully "
```

---

### Task 2: PR Validation Workflow
Create `.github/workflows/pr-checks.yml` — a real-world PR gate:
1. Trigger on `pull_request` to `main`
2. Add a job `file-size-check` that:
   - Checks out the code
   - Fails if any file in the PR is larger than 1 MB
3. Add a job `branch-name-check` that:
   - Reads the branch name from `${{ github.head_ref }}`
   - Fails if it doesn't follow the pattern `feature/*`, `fix/*`, or `docs/*`
4. Add a job `pr-body-check` that:
   - Reads the PR body: `${{ github.event.pull_request.body }}`
   - Warns (but doesn't fail) if the PR description is empty

**Verify:** Open a PR from a badly named branch — does the check fail?

```
name: PR Checks

on:
  pull_request:
    branches: [main]

jobs:
  file-size-check:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Check file sizes
        run: |
          files=$(git diff --name-only origin/main)
          for file in $files; do
            if [ -f "$file" ]; then
              size=$(stat -c%s "$file")
              if [ $size -gt 1048576 ]; then
                echo "File $file is larger than 1MB"
                exit 1
              fi
            fi
          done

  branch-name-check:
    runs-on: ubuntu-latest

    steps:
      - name: Validate branch name
        run: |
          echo "Branch: ${{ github.head_ref }}"
          if [[ ! "${{ github.head_ref }}" =~ ^(feature|fix|docs)/ ]]; then
            echo "Invalid branch name!"
            exit 1
          fi

  pr-body-check:
    runs-on: ubuntu-latest

    steps:
      - name: Check PR body
        run: |
          if [ -z "${{ github.event.pull_request.body }}" ]; then
            echo "WARNING: PR description is empty"
          else
            echo "PR description exists"
          fi
```
---

### Task 3: Scheduled Workflows (Cron Deep Dive)
Create `.github/workflows/scheduled-tasks.yml`:
1. Add a `schedule` trigger with cron: `'30 2 * * 1'` (every Monday at 2:30 AM UTC)
2. Add **another** cron entry: `'0 */6 * * *'` (every 6 hours)
3. In the job, print which schedule triggered using `${{ github.event.schedule }}`
4. Add a step that acts as a **health check** — curl a URL and check the response code

Write in your notes:
- The cron expression for: every weekday at 9 AM IST
  - 30 3 * * 1-5
- The cron expression for: first day of every month at midnight
  - 0 0 1 * *
- Why GitHub says scheduled workflows may be delayed or skipped on inactive repos
  - GitHub reduces runs for inactive repositories
  - Load balancing on GitHub Actions servers
  - No recent repo activity = cron may pause

**Important:** Also add `workflow_dispatch` so you can test it manually without waiting for the schedule.

```
name: Scheduled Tasks

on:
  schedule:
    - cron: '30 2 * * 1'
    - cron: '0 */6 * * *'
  workflow_dispatch:

jobs:
  scheduled-job:
    runs-on: ubuntu-latest

    steps:
      - name: Print schedule
        run: echo "Triggered by: ${{ github.event.schedule }}"

      - name: Health check
        run: |
          STATUS=$(curl -o /dev/null -s -w "%{http_code}" https://example.com)
          echo "Status Code: $STATUS"
          if [ "$STATUS" -ne 200 ]; then
            echo "Health check failed"
            exit 1
          fi
```
---

### Task 4: Path & Branch Filters
Create `.github/workflows/smart-triggers.yml`:
1. Trigger on push but **only** when files in `src/` or `app/` change:
   ```yaml
   on:
     push:
       paths:
         - 'src/**'
         - 'app/**'
   ```
2. Add `paths-ignore` in a second workflow that skips runs when only docs change:
   ```yaml
   paths-ignore:
     - '*.md'
     - 'docs/**'
   ```
3. Add branch filters to only trigger on `main` and `release/*` branches
4. Test it: push a change to a `.md` file — does the workflow skip?

Write in your notes: When would you use `paths` vs `paths-ignore`?

- paths vs paths-ignore
  - paths → run workflow ONLY when specific files change
  - paths-ignore → skip workflow when only certain files change

```
name: Smart Trigger

on:
  push:
    branches:
      - main
      - 'release/*'
    paths:
      - 'src/**'
      - 'app/**'

jobs:
  run-on-code-change:
    runs-on: ubuntu-latest

    steps:
      - run: echo "Code changed in src/ or app/"
```

```
name: Ignore Docs Changes

on:
  push:
    paths-ignore:
      - '*.md'
      - 'docs/**'

jobs:
  skip-docs:
    runs-on: ubuntu-latest

    steps:
      - run: echo "Triggered because non-doc files changed"
```

---

### Task 5: `workflow_run` — Chain Workflows Together
Create two workflows:
1. `.github/workflows/tests.yml` — runs tests on every push
2. `.github/workflows/deploy-after-tests.yml` — triggers **only after** `tests.yml` completes successfully:
   ```yaml
   on:
     workflow_run:
       workflows: ["Run Tests"]
       types: [completed]
   ```
3. In the deploy workflow, add a conditional:
   - Only proceed if the triggering workflow **succeeded** (`${{ github.event.workflow_run.conclusion == 'success' }}`)
   - Print a warning and exit if it failed

**Verify:** Push a commit — does the test workflow run first, then trigger the deploy workflow?

### workflow_run vs workflow_call

- workflow_run
  - Triggers AFTER another workflow finishes
  - Used for pipeline chaining (test → deploy)

- workflow_call
  - Reusable workflow
  - Called INSIDE another workflow like a function

```
name: Run Tests

on:
  push:

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Run dummy test
        run: echo "Tests passed"
```

```
name: Deploy After Tests

on:
  workflow_run:
    workflows: ["Run Tests"]
    types: [completed]

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Check result
        if: github.event.workflow_run.conclusion == 'success'
        run: echo "Deploying because tests passed 🚀"

      - name: Fail if tests failed
        if: github.event.workflow_run.conclusion != 'success'
        run: |
          echo "Tests failed. Skipping deploy."
          exit 1
```
---

### Task 6: `repository_dispatch` — External Event Triggers
1. Create `.github/workflows/external-trigger.yml` with trigger `repository_dispatch`
2. Set it to respond to event type: `deploy-request`
3. Print the client payload: `${{ github.event.client_payload.environment }}`
4. Trigger it using `curl` or `gh`:
   ```bash
   gh api repos/<owner>/<repo>/dispatches \
     -f event_type=deploy-request \
     -f client_payload='{"environment":"production"}'
   ```

Write in your notes: When would an external system (like a Slack bot or monitoring tool) trigger a pipeline?

- Used when:
  - Slack bot triggers deploy
  - Monitoring system detects downtime
  - External CI/CD tool triggers pipeline
    
```

name: External Trigger

on:
  repository_dispatch:
    types: [deploy-request]

jobs:
  external:
    runs-on: ubuntu-latest

    steps:
      - name: Print payload
        run: echo "Environment: ${{ github.event.client_payload.environment }}"

```
---

✅ FINAL CHECKLIST

✔ PR lifecycle workflow
✔ PR validation checks
✔ Scheduled cron workflow
✔ Path filters
✔ Workflow chaining
✔ External trigger
✔ Markdown documentation

---

## Hints
- PR merge check: `if: github.event.pull_request.merged == true`
- Cron syntax: `minute hour day-of-month month day-of-week`
- Scheduled workflows only run on the **default branch**
- `workflow_run` gives you access to the triggering workflow's conclusion and artifacts
- `repository_dispatch` requires a personal access token with `repo` scope
- Path filters use glob patterns — `**` matches nested directories
