# Day 40 – Your First GitHub Actions Workflow

## Challenge Tasks

### Task 1: Set Up
1. Create a new **public** GitHub repository called `github-actions-practice`
2. Clone it locally
3. Create the folder structure: `.github/workflows/`

<img width="1474" height="604" alt="image" src="https://github.com/user-attachments/assets/50cf88a8-17a9-4484-96c8-a496eca045dd" />

---

### Task 2: Hello Workflow
Create `.github/workflows/hello.yml` with a workflow that:
1. Triggers on every `push`
2. Has one job called `greet`
3. Runs on `ubuntu-latest`
4. Has two steps:
   - Step 1: Check out the code using `actions/checkout`
   - Step 2: Print `Hello from GitHub Actions!`
  
```

name: hello-github

on:
 push:
   branches: [main]

jobs:

  greet:
    runs-on: ubuntu-latest
    steps:
      - name: checkout code
        uses: actions/checkout@v4
      - name: greeting
        run: echo "Hello from Github Actions"
```

Push it. Go to the **Actions** tab on GitHub and watch it run.

<img width="2914" height="1104" alt="image" src="https://github.com/user-attachments/assets/a796b9e2-584a-43ef-8a36-7a2a20034f28" />


**Verify:** Is it green? Click into the job and read every step.

---

### Task 3: Understand the Anatomy
Look at your workflow file and write in your notes what each key does:
- `on:`
- `jobs:`
- `runs-on:`
- `steps:`
- `uses:`
- `run:`
- `name:` (on a step)

| Key        | Purpose                          |
| ---------- | -------------------------------- |
| `on:`      | Defines when the workflow starts |
| `jobs:`    | Defines jobs in the workflow     |
| `runs-on:` | Specifies the runner machine     |
| `steps:`   | Lists tasks inside a job         |
| `uses:`    | Runs a prebuilt GitHub Action    |
| `run:`     | Executes shell commands          |
| `name:`    | Labels a step for readability    |

---

### Task 4: Add More Steps
Update `hello.yml` to also:
1. Print the current date and time
2. Print the name of the branch that triggered the run (hint: GitHub provides this as a variable)
3. List the files in the repo
4. Print the runner's operating system
```
name: hello-github

on:
 push:
   branches: [main]

jobs:

  greet:
    runs-on: ubuntu-latest
    steps:
      - name: time and date
        run: date
      - name: Print the branch name using an environment variable
        run: echo "The branch that triggered this run is $GITHUB_REF_NAME"
      - name: list file in repo
        run: ls -la
      - name: checkout code
        uses: actions/checkout@v4
      - name: greeting
        run: echo "Hello from Github Actions"
      - name: runner os 
        run: echo "runner os is $RUNNER_OS"
```
Push again — watch the new run.

<img width="2892" height="1404" alt="image" src="https://github.com/user-attachments/assets/cac8d476-18de-46b0-9cc9-ecb005fc7caf" />

---

### Task 5: Break It On Purpose
1. Add a step that runs a command that will **fail** (e.g., `exit 1` or a misspelled command)
2. Push and observe what happens in the Actions tab
3. Fix it and push again

Write in your notes: What does a failed pipeline look like? How do you read the error?

```
# error note
Run python--version
/home/runner/work/_temp/22312b3b-593b-4a47-a1dc-57803a34ef33.sh: line 1: python--version: command not found
Error: Process completed with exit code 127.
```
- fixed the command and it starts working again . 

<img width="2892" height="1316" alt="image" src="https://github.com/user-attachments/assets/80e7d01b-5ac4-4b27-b3b7-35b4a906da19" />


---

## Hints
- Workflow files live in `.github/workflows/` and must end in `.yml`
- `uses: actions/checkout@v4` checks out your code onto the runner
- `run:` executes shell commands
- GitHub provides built-in variables like `${{ github.ref_name }}` for branch name
- Every push triggers a new run — check the Actions tab

---

## Documentation
Create `day-40-first-workflow.md` with:
- Your workflow YAML
- Screenshot of the green run
- What each `on:`, `jobs:`, `steps:` key does (your own words)

---

