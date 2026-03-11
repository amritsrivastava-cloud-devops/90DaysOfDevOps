# Day 41 – Triggers & Matrix Builds

## Challenge Tasks

### Task 1: Trigger on Pull Request
1. Create `.github/workflows/pr-check.yml`
2. Trigger it only when a pull request is **opened or updated** against `main`
3. Add a step that prints: `PR check running for branch: <branch name>`
4. Create a new branch, push a commit, and open a PR
5. Watch the workflow run automatically

**Verify:** Does it show up on the PR page?

```
name: PR Check

on:
  pull_request:
    branches: [ main ]
    types: [opened, synchronize]

jobs:
  pr-check:
    runs-on: ubuntu-latest

    steps:
      - name: Print PR branch
        run: echo "PR check running for branch: ${{ github.head_ref }}"
```

---

### Task 2: Scheduled Trigger
1. Add a `schedule:` trigger to any workflow using cron syntax
2. Set it to run every day at midnight UTC
3. Write in your notes: What is the cron expression for every Monday at 9 AM?

```
on:
  schedule:
    - cron: '0 9 * * 1'
```
---

### Task 3: Manual Trigger
1. Create `.github/workflows/manual.yml` with a `workflow_dispatch:` trigger
2. Add an **input** that asks for an `environment` name (staging/production)
3. Print the input value in a step
4. Go to the **Actions** tab → find the workflow → click **Run workflow**

**Verify:** Can you trigger it manually and see your input printed?

```
name: Manual Workflow

on:
  workflow_dispatch:
    inputs:
      environment:
        description: "Choose environment"
        required: true
        default: "staging"

jobs:
  manualwork:
    runs-on: ubuntu-latest

    steps:
      - name: Print environment 
        run: echo "Running deployment for environment"
```
<img width="2926" height="1082" alt="image" src="https://github.com/user-attachments/assets/3f7cd8af-a2ff-4fe8-83d2-ef0038b82b10" />

---

### Task 4: Matrix Builds
Create `.github/workflows/matrix.yml` that:
1. Uses a matrix strategy to run the same job across:
   - Python versions: `3.10`, `3.11`, `3.12`
2. Each job installs Python and prints the version
3. Watch all 3 run in parallel

Then extend the matrix to also include 2 operating systems — how many total jobs run now?

```
name: Matrix Python

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  Python-validation:
    runs-on: ubuntu-latest
    strategy:
      fail-fast:
      matrix:
        python-version: ["3.10", "3.11", "3.12"]

    steps:
      - name: checkout repository
        uses: actions/checkout@v4
      - name: setup python
        uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version}}
      - name: python version printing
        run: python --version

```

<img width="2308" height="1202" alt="image" src="https://github.com/user-attachments/assets/d78de61a-4d14-45cd-946b-7d70988f3608" />

---

### Task 5: Exclude & Fail-Fast
1. In your matrix, **exclude** one specific combination (e.g., Python 3.10 on Windows)
2. Set `fail-fast: false` — trigger a failure in one job and observe what happens to the rest
3. Write in your notes: What does `fail-fast: true` (the default) do vs `false`?

```
name: Matrix Exclude FailFast Test

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  matrix-test:
    runs-on: ${{ matrix.os }}

    strategy:
      fail-fast: false
      matrix:
        os: [ubuntu-latest, windows-latest]
        python-version: ["3.10", "3.11", "3.12"]

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}

      - name: Print Python Version
        run: python --version

      - name: Fail only on Windows Python 3.10
        if: matrix.os == 'windows-latest' && matrix.python-version == '3.10'
        run: exit 1
```

<img width="2316" height="1122" alt="image" src="https://github.com/user-attachments/assets/f639da4a-4eb0-4650-94d4-7ddf3ed2dec7" />

<img width="2318" height="1060" alt="image" src="https://github.com/user-attachments/assets/bc030e9e-c00a-4a44-87de-572fc464ecb1" />


---

## Hints
- PR trigger: `on: pull_request: branches: [main]`
- Cron trigger: `on: schedule: - cron: '0 0 * * *'`
- Manual trigger: `on: workflow_dispatch: inputs:`
- Matrix: `strategy: matrix: python-version: [...]`
- Exclude: `exclude: - os: windows-latest python-version: "3.10"`

---

## Documentation
Create `day-41-triggers.md` with:
- Each workflow YAML
- Screenshots of runs
- The cron expression answer from Task 2

---
