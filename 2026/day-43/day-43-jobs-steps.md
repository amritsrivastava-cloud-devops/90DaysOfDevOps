# Day 43 – Jobs, Steps, Env Vars & Conditionals

## Challenge Tasks

### Task 1: Multi-Job Workflow
Create `.github/workflows/multi-job.yml` with 3 jobs:
- `build` — prints "Building the app"
- `test` — prints "Running tests"
- `deploy` — prints "Deploying"

Make `test` run only **after** `build` succeeds.
Make `deploy` run only **after** `test` succeeds.

```
name: Multi jobs

on:
 workflow_dispatch: 

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: build application
        run: echo "building the app"
        
  test:
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: testing the application
        run: echo "testing the application"
        
  deploy:
    runs-on: ubuntu-latest
    needs: test
    steps:
      - name: deploying onto prod
        run: echo "deployment sucessfully completed"
  
  ```

**Verify:** Check the workflow graph in the Actions tab — does it show the dependency chain?


---

### Task 2: Environment Variables
In a new workflow, use environment variables at 3 levels:
1. **Workflow level** — `APP_NAME: myapp`
2. **Job level** — `ENVIRONMENT: staging`
3. **Step level** — `VERSION: 1.0.0`

Print all three in a single step and verify each is accessible.

Then use a **GitHub context variable** — print the commit SHA and the actor (who triggered the run).

```
name: Environment Variables

on:
  workflow_dispatch:

env:
  APP_NAME: myapp

jobs:
  environment-variable:
    runs-on: ubuntu-latest
    env:
      ENVIRONMENT: staging

    steps:
      - name: Print Variables
        env:
          VERSION: 1.0.0
        run: |
          echo "App Name: $APP_NAME"
          echo "Environment: $ENVIRONMENT"
          echo "Version: $VERSION"
          echo "Commit SHA: ${{ github.sha }}"
          echo "Triggered By: ${{ github.actor }}"

```
---

### Task 3: Job Outputs
1. Create a job that **sets an output** — e.g., today's date as a string
2. Create a second job that **reads that output** and prints it
3. Pass the value using `outputs:` and `needs.<job>.outputs.<name>`

## Why pass outputs between jobs?

Passing outputs between jobs allows one job to generate data that another job can use later in the workflow.

Since GitHub Actions jobs run on separate runners, they do not automatically share variables or data. Using `outputs` allows controlled communication between jobs.

### Example Use Cases
- Passing a **build version or image tag** from a build job to a deploy job
- Sharing a **generated artifact name or file path**
- Passing **test results or status information**
- Sending **dynamic values** like timestamps, commit information, or environment names

### Example Flow
Build Job → generates a Docker image tag  
Deploy Job → reads that tag and deploys the same image

This ensures that different stages of the pipeline stay **consistent and use the same generated values**.

```

name: Job Outputs

on:
  workflow_dispatch:

jobs:

  set-output:
    runs-on: ubuntu-latest

    outputs:
      today: ${{ steps.setdate.outputs.today }}

    steps:
      - name: Generate todays date
        id: setdate
        run: echo "today=$(date)" >> $GITHUB_OUTPUT

  print-output:
    runs-on: ubuntu-latest

    needs: set-output

    steps:
      - name: print date from previous job
        run: echo "Today's date is ${{ needs.set-output.outputs.today }}"

```

---

### Task 4: Conditionals
In a workflow, add:
1. A step that only runs when the branch is `main`
2. A step that only runs when the previous step **failed**
3. A job that only runs on **push** events, not on pull requests
4. A step with `continue-on-error: true` — what does this do?


```

name: Conditional Workflow

on:
  push:
  pull_request:

jobs:

  conditional-job:
    runs-on: ubuntu-latest

    if: github.event_name == 'push'

    steps:

      - name: Run only on main branch
        if: github.ref == 'refs/heads/main'
        run: echo "This step runs only on main branch"

      - name: Intentional failure
        run: exit 1

      - name: Run when previous step fails
        if: failure()
        run: echo "Previous step failed"

      - name: Continue on error example
        continue-on-error: true
        run: |
          echo "This step will fail but workflow continues"
          exit 1

```

---

### Task 5: Putting It Together
Create `.github/workflows/smart-pipeline.yml` that:
1. Triggers on push to any branch
2. Has a `lint` job and a `test` job running in parallel
3. Has a `summary` job that runs after both, prints whether it's a `main` branch push or a feature branch push, and prints the commit message

```
name: Smart Pipeline

on:
  push:
    branches:
      - "**"

jobs:

  lint:
    runs-on: ubuntu-latest
    steps:
      - name: Run lint
        run: echo "Running lint checks"

  test:
    runs-on: ubuntu-latest
    steps:
      - name: Run tests
        run: echo "Running tests"

  summary:
    runs-on: ubuntu-latest
    needs: [lint, test]

    steps:
      - name: Check branch type
        run: |
          if [[ "${{ github.ref }}" == "refs/heads/main" ]]; then
           echo "Main branch push"
          else
           echo "Feature branch push"
          fi

      - name: Print commit message
        run: echo "Commit message:${{ github.event.commits[0].message }}"

```
---

## Hints
- Job dependency: `needs: [job-name]`
- Set output: `echo "date=$(date)" >> $GITHUB_OUTPUT`
- Read output: `${{ needs.job-name.outputs.date }}`
- Conditionals: `if: github.ref == 'refs/heads/main'`
- Commit message: `${{ github.event.commits[0].message }}`
