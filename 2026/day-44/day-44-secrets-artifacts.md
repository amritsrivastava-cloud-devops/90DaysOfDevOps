# Day 44 – Secrets, Artifacts & Running Real Tests in CI

---
## Challenge Tasks

### Task 1: GitHub Secrets
1. Go to your repo → Settings → Secrets and Variables → Actions
2. Create a secret called `MY_SECRET_MESSAGE`
3. Create a workflow that reads it and prints: `The secret is set: true` (never print the actual value)
4. Try to print `${{ secrets.MY_SECRET_MESSAGE }}` directly — what does GitHub show?

Write in your notes: Why should you never print secrets in CI logs?

```
name: Secret Message

on:
  workflow_dispatch:

jobs:

  show-secret-message:
    runs-on: ubuntu-latest
    steps:
      - name: check if secret exist
        run: |
          if [ -z "${{ secrets.MY_SECRET_MESSAGE }}" ]; then
            echo "Secret not set"
          else
            echo "The secret is set: true"
          fi

      - name: Attempt to print secret
        run: echo "Secret value is:${{ secrets.MY_SECRET_MESSAGE }}"
```

- What GitHub shows
  - GitHub masks the secret in logs like this:
  - Secret value is: ***

- Why never print secrets?

  - Secrets may contain API keys, passwords, tokens
  - CI logs are visible to collaborators
  - Exposing them can allow unauthorized access to infrastructure
  - Attackers could deploy code, delete resources, or steal data
    
---

### Task 2: Use Secrets as Environment Variables
1. Pass a secret to a step as an environment variable
2. Use it in a shell command without ever hardcoding it
3. Add `DOCKER_USERNAME` and `DOCKER_TOKEN` as secrets (you'll need these on Day 45)

```
name: env-secrets

on:
  workflow_dispatch: 

jobs:
  use-env-secret:
    runs-on: ubuntu-latest

    steps:
      - name: Use secret as env variable
        env:
          DOCKER_USERNAME: ${{ secrets.DOCKER_USERNAME }}
          DOCKER_TOKEN: ${{ secrets.DOCKER_TOKEN }}

        run: |
          echo "Docker username is set"
          echo "Token length: ${#DOCKER_TOKEN}"
```
- Secrets are not hardcoded and not printed directly.

```
# artifacts-demo.yml

```
---

### Task 3: Upload Artifacts
1. Create a step that generates a file — e.g., a test report or a log file
2. Use `actions/upload-artifact` to save it
3. After the workflow runs, download the artifact from the Actions tab

**Verify:** Can you see and download it from GitHub?

```
name: artifacts-demo

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Create report file
        run: |
          echo "ci test report" > report.txt
          echo "build sucecessful" >> report.txt

      - name: upload artifact
        uses: actions/upload-artifact@v4
        with:
          name: test-report
          path: report.txt

  consume:
    runs-on: ubuntu-latest
    needs: build

    steps:
      - name: download artifact
        uses: actions/download-artifact@v4
        with:
          name: test-report

      - name: print artifact content
        run: cat report.txt
    
```

**GitHub Repo → Actions → Workflow Run → Artifacts**
---

### Task 4: Download Artifacts Between Jobs
1. Job 1: generate a file and upload it as an artifact
2. Job 2: download the artifact from Job 1 and use it (print its contents)

```
name: artifact-between-jobs

on:
  push:
    branches: [ main ]

jobs:
  generate-file:
    runs-on: ubuntu-latest

    steps:
      - name: Create a file
        run: |
          echo "Hello from Job 1" > message.txt
          echo "Artifact created in CI pipeline" >> message.txt

      - name: Upload artifact
        uses: actions/upload-artifact@v4
        with:
          name: message-file
          path: message.txt


  use-artifact:
    runs-on: ubuntu-latest
    needs: generate-file

    steps:
      - name: Download artifact
        uses: actions/download-artifact@v4
        with:
          name: message-file

      - name: Print file contents
        run: cat message.txt
```

- Write in your notes: When would you use artifacts in a real pipeline?
  - Artifacts are used to store and transfer files between jobs or after a workflow run.
---

### Task 5: Run Real Tests in CI
Take any script from your earlier days (Python or Shell) and run it in CI:
1. Add your script to the `github-actions-practice` repo
2. Write a workflow that:
   - Checks out the code
   - Installs any dependencies needed
   - Runs the script
   - Fails the pipeline if the script exits with a non-zero code
3. Intentionally break the script — verify the pipeline goes red
4. Fix it — verify it goes green again

```
# test.sh

#!/bin/bash

echo "Running CI tests..."

# simple test
if [ 10 -gt 5 ]; then
  echo "Test Passed"
  exit 0
else
  echo "Test Failed"
  exit 1
fi

```

```
name: Run Real Tests

on:
  push:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Make script executable
        run: chmod +x scripts/test.sh

      - name: Run test script
        run: ./scripts/test.sh

```

---

### Task 6: Caching
1. Add `actions/cache` to a workflow that installs dependencies
2. Run it twice — observe the time difference
3. Write in your notes: What is being cached and where is it stored?

```
name: cache-demo

on:
  push:

jobs:
  cache-example:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.11"

      - name: Cache pip dependencies
        uses: actions/cache@v4
        with:
          path: ~/.cache/pip
          key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}

      - name: Install dependencies
        run: pip install -r requirements.txt

```
- What is cached?
  - Python packages installed via pip
  - Stored in GitHub's cache storage
  - Restored in future workflow runs if cache key matches

 
---

## Hints
- Secrets: `${{ secrets.SECRET_NAME }}`
- Upload artifact: `uses: actions/upload-artifact@v4`
- Download artifact: `uses: actions/download-artifact@v4`
- Cache: `uses: actions/cache@v4`
- GitHub masks secret values in logs automatically

---
