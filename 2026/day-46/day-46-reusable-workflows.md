# Day 46 – Reusable Workflows & Composite Actions

## Challenge Tasks

### Task 1: Understand `workflow_call`
Before writing any code, research and answer in your notes:
1. What is a **reusable workflow**?
   - A reusable workflow is a GitHub Actions workflow that can be called from another workflow to reuse the same CI/CD logic across multiple workflows or repositories.
     - Instead of duplicating jobs, you define them once and call them whenever needed.
   - Example use cases:
    - Build pipelines
    - Docker build logic
    - Security scans
    - Deployment pipelines
      
2. What is the `workflow_call` trigger?
   - workflow_call allows a workflow to be triggered by another workflow.
     ```
     on:
       workflow_call:
     ```
   - This means the workflow cannot run directly — it only runs when another workflow calls it.
  
3. How is calling a reusable workflow different from using a regular action (`uses:`)?

| Feature  | Reusable Workflow | Regular Action          |
| -------- | ----------------- | ----------------------- |
| Level    | Workflow level    | Step level              |
| Contains | Multiple jobs     | One step or small logic |
| Trigger  | `workflow_call`   | `uses:` in a step       |
| Use case | Full pipelines    | Small reusable tasks    |

Example:

Reusable workflow
```
jobs:
  build:
    uses: ./.github/workflows/reusable-build.yml
```
Action
```
steps:
  - uses: actions/checkout@v4
```
4. Where must a reusable workflow file live?

- It must be inside
```
.github/workflows/

Example:

.github/workflows/reusable-build.yml
```

---

### Task 2: Create Your First Reusable Workflow
Create `.github/workflows/reusable-build.yml`:
1. Set the trigger to `workflow_call`
2. Add an `inputs:` section with:
   - `app_name` (string, required)
   - `environment` (string, required, default: `staging`)
3. Add a `secrets:` section with:
   - `docker_token` (required)
4. Create a job that:
   - Checks out the code
   - Prints `Building <app_name> for <environment>`
   - Prints `Docker token is set: true` (never print the actual secret)

**Verify:** This file alone won't run — it needs a caller. That's next.

```
name: Reusable Build Workflow

on:
  workflow_call:
    inputs:
      app_name:
        required: true
        type: string
      environment:
        required: true
        type: string
        default: staging

    secrets:
      docker_token:
        required: true

    outputs:
      build_version:
        value: ${{ jobs.build.outputs.build_version }}

jobs:
  build:
    runs-on: ubuntu-latest

    outputs:
      build_version: ${{ steps.version.outputs.build_version }}

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Print build info
        run: |
          echo "Building ${{ inputs.app_name }} for ${{ inputs.environment }}"

      - name: Check docker token
        run: |
          echo "Docker token is set: ${{ secrets.docker_token != '' }}"

      - name: Generate version
        id: version
        run: |
          VERSION="v1.0-${GITHUB_SHA::7}"
          echo "build_version=$VERSION" >> $GITHUB_OUTPUT
```
---

### Task 3: Create a Caller Workflow
Create `.github/workflows/call-build.yml`:
1. Trigger on push to `main`
2. Add a job that uses your reusable workflow:
   ```yaml
   jobs:
     build:
       uses: ./.github/workflows/reusable-build.yml
       with:
         app_name: "my-web-app"
         environment: "production"
       secrets:
         docker_token: ${{ secrets.DOCKER_TOKEN }}
   ```
3. Push to `main` and watch it run

**Verify:** In the Actions tab, do you see the caller triggering the reusable workflow? Click into the job — can you see the inputs printed?

```
name: Call Reusable Build

on:
  push:
    branches:
      - main

jobs:
  build:
    uses: ./.github/workflows/reusable-build.yml
    with:
      app_name: "my-web-app"
      environment: "production"
    secrets:
      docker_token: ${{ secrets.DOCKER_TOKEN }}

  print-version:
    runs-on: ubuntu-latest
    needs: build

    steps:
      - name: Print build version
        run: echo "Build version is ${{ needs.build.outputs.build_version }}"
```
---

### Task 4: Add Outputs to the Reusable Workflow
Extend `reusable-build.yml`:
1. Add an `outputs:` section that exposes a `build_version` value
2. Inside the job, generate a version string (e.g., `v1.0-<short-sha>`) and set it as output
3. In your caller workflow, add a second job that:
   - Depends on the build job (`needs:`)
   - Reads and prints the `build_version` output

**Verify:** Does the second job print the version from the reusable workflow?

```
Reusable workflow
        ↓
job output
        ↓
workflow output
        ↓
caller workflow
        ↓
next job
```
---

### Task 5: Create a Composite Action
Create a **custom composite action** in your repo at `.github/actions/setup-and-greet/action.yml`:
1. Define inputs: `name` and `language` (default: `en`)
2. Add steps that:
   - Print a greeting in the specified language
   - Print the current date and runner OS
   - Set an output called `greeted` with value `true`
3. Use the composite action in a new workflow with `uses: ./.github/actions/setup-and-greet`

**Verify:** Does your custom action run and print the greeting?

```
name: Setup and Greet

description: Simple greeting composite action

inputs:
  name:
    required: true
    description: Person name
  language:
    required: false
    default: en
    description: Greeting language

outputs:
  greeted:
    value: true

runs:
  using: "composite"

  steps:
    - name: Greeting
      shell: bash
      run: |
        if [ "${{ inputs.language }}" == "en" ]; then
          echo "Hello ${{ inputs.name }}"
        elif [ "${{ inputs.language }}" == "es" ]; then
          echo "Hola ${{ inputs.name }}"
        else
          echo "Hello ${{ inputs.name }}"
        fi

    - name: Print date and OS
      shell: bash
      run: |
        echo "Date: $(date)"
        echo "Runner OS: $RUNNER_OS"

    - name: Set output
      shell: bash
      run: echo "greeted=true" >> $GITHUB_OUTPUT
```

```
name: Greeting Workflow

on:
  push:

jobs:
  greet:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Run custom greeting action
        id: greet
        uses: ./.github/actions/setup-and-greet
        with:
          name: Amrit
          language: en

      - name: Check output
        run: echo "Greeting completed: ${{ steps.greet.outputs.greeted }}"
```
---

### Task 6: Reusable Workflow vs Composite Action
Fill this in your notes:

|                              | Reusable Workflow    | Composite Action                 |
| ---------------------------- | -------------------- | -------------------------------- |
| Triggered by                 | `workflow_call`      | `uses:` in a step                |
| Can contain jobs?            | Yes                  | No                               |
| Can contain multiple steps?  | Yes                  | Yes                              |
| Lives where?                 | `.github/workflows/` | `.github/actions/<action-name>/` |
| Can accept secrets directly? | Yes                  | No                               |
| Best for                     | Full CI/CD pipelines | Reusable step logic              |


---

## Hints
- Reusable workflows must be in `.github/workflows/` directory
- Caller syntax: `uses: ./.github/workflows/file.yml` (same repo) or `uses: org/repo/.github/workflows/file.yml@main` (cross-repo)
- Composite action: `action.yml` with `runs: using: "composite"`
- Reusable workflow outputs: `on: workflow_call: outputs: name: value: ${{ jobs.job-id.outputs.name }}`
- A reusable workflow can be called by at most 20 unique caller workflows in a single run

---

✅ Concept Summary

- Use Reusable Workflow when:
  - You want to reuse entire pipelines
  - Multiple jobs required
  - CI/CD templates

- Use Composite Action when:
  - Reusing a set of steps
  - Custom mini-action
  - Reusable scripts
