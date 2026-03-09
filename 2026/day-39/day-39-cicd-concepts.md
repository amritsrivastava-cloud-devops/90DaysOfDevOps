# Day 39 – What is CI/CD?

## Task
Before writing a single pipeline, understand **why CI/CD exists** and what it actually does.

Today is a research and diagram day — no pipelines yet. Get the concepts right first.

---

## Challenge Tasks

### Task 1: The Problem
Think about a team of 5 developers all pushing code to the same repo manually deploying to production.

Write in your notes:
1. What can go wrong?
```
Code from different developers may conflict.
Bugs may reach production because testing is manual.
One developer might overwrite another developer’s work.
Deployment steps may be forgotten or done incorrectly.
Production environment may break due to inconsistent setup.
```
2. What does "it works on my machine" mean and why is it a real problem?
```
This means the code works correctly on the developer’s local computer but fails in another environment such as staging or production.
Reasons:
Different OS
Different dependency versions
Missing environment variables
Different configuration files
This becomes a real problem because software must run consistently across environments.
```
3. How many times a day can a team safely deploy manually?
```
Usually 1–2 times per day at most, because manual deployments are:
Slow
Error-prone
Risky without automation
This is why automation through CI/CD pipelines becomes necessary.
```
---

### Task 2: CI vs CD
Research and write short definitions (2-3 lines each):
1. **Continuous Integration** — what happens, how often, what it catches
```
Continuous Integration is the practice where developers frequently merge code into a shared repository.
Every commit triggers an automated process that builds the project and runs tests to detect errors early.

Example
A developer pushes code to GitHub →
GitHub Actions automatically:
installs dependencies
runs tests
verifies the build
If tests fail, the pipeline stops.

```
2. **Continuous Delivery** — how it's different from CI, what "delivery" means
```
Continuous Delivery ensures that the codebase is always ready to be deployed to production.
After CI completes successfully, the application is built and prepared for deployment, but deployment usually requires manual approval.

Example
Pipeline flow:

Push → Build → Test → Create Docker Image → Ready for Production

A team member approves before deploying.
```
3. **Continuous Deployment** — how it differs from Delivery, when teams use it
```
Continuous Deployment automatically deploys every successful change directly to production without human approval.

Only companies with strong testing and monitoring typically use this.

Example
Pipeline flow:

Push → Build → Test → Deploy to Production automatically

Companies like Netflix and Facebook deploy many times per day using this approach.
```
Write one real-world example for each.

---

### Task 3: Pipeline Anatomy
A pipeline has these parts — write what each one does:
- **Trigger** — what starts the pipeline
```
A trigger is the event that starts a pipeline.

Examples:

Code push
Pull request
Scheduled job
Manual trigger

Example:

on: push

```
- **Stage** — a logical phase (build, test, deploy)
```
A stage is a logical phase of the pipeline.

Common stages:
Build
Test
Deploy

Stages help organize the pipeline workflow.
```
- **Job** — a unit of work inside a stage
```
A job is a group of steps executed on the same machine.

Example job types:

build job
test job
docker build job

Jobs inside a stage can run sequentially or in parallel.
```
- **Step** — a single command or action inside a job
```
A step is a single command or action executed inside a job.

Examples:

npm install
npm test
docker build

Each job contains multiple steps.
```
- **Runner** — the machine that executes the job
```
A runner is the machine that executes the pipeline jobs.

Examples:

GitHub hosted runner
Self-hosted runner
Jenkins agent

The runner provides CPU, memory, and environment for execution.
```
- **Artifact** — output produced by a job
```
Artifacts are files produced by a pipeline job and stored for later use.

Examples:

compiled binaries
test reports
Docker images
build packages

Artifacts allow later stages to use outputs from previous stages.
```

---

### Task 4: Draw a Pipeline
Draw a CI/CD pipeline for this scenario:
> A developer pushes code to GitHub. The app is tested, built into a Docker image, and deployed to a staging server.

Include at least 3 stages. Hand-drawn and photographed is perfectly fine.

Developer
   |
   v
Push Code to GitHub
   |
   v
+---------------------+
|      TRIGGER        |
|     (git push)      |
+---------------------+
          |
          v

+---------------------+
|      STAGE 1        |
|        BUILD        |
| install dependencies|
| compile application |
+---------------------+
          |
          v

+---------------------+
|      STAGE 2        |
|        TEST         |
| run unit tests      |
| run integration     |
+---------------------+
          |
          v

+---------------------+
|      STAGE 3        |
|   DOCKER BUILD      |
| docker build image  |
| push to registry    |
+---------------------+
          |
          v

+---------------------+
|      STAGE 4        |
|      DEPLOY         |
| deploy to staging   |
+---------------------+

---

### Task 5: Explore in the Wild
1. Open any popular open-source repo on GitHub (Kubernetes, React, FastAPI — pick one you know)
2. Find their `.github/workflows/` folder
3. Open one workflow YAML file
4. Write in your notes:
   - What triggers it?
   - How many jobs does it have?
   - What does it do? (best guess)
  
```
# using .github/workflows/addtoproject.yml for fastapi github repo
Workflow Analysis (FastAPI)

Workflow file:
.github/workflows/add-to-project.yml

What triggers it?
The workflow is triggered when:
A pull request event occurs (pull_request_target)
An issue is opened
An issue is reopened
So whenever someone creates or reopens an issue, or interacts with a pull request, the workflow starts automatically.

## How many jobs does it have?

The workflow contains 1 job:

add-to-project
This job runs on a GitHub runner (ubuntu-latest).

What does it do? (Best guess)
The workflow automatically adds newly created issues or pull requests to the FastAPI GitHub project board.

It uses a GitHub Action:
actions/add-to-project@v1.0.2

This action takes the issue or pull request and adds it to the FastAPI project management board, helping maintainers organize and track tasks.

########CODE########

name: Add to Project

on:
  pull_request_target:
  issues:
    types:
      - opened
      - reopened

jobs:
  add-to-project:
    name: Add to project
    runs-on: ubuntu-latest
    steps:
      - uses: actions/add-to-project@v1.0.2
        with:
          project-url: https://github.com/orgs/fastapi/projects/2
          github-token: ${{ secrets.PROJECTS_TOKEN }}

```

---

## Hints
- CI/CD is a practice, not just a tool
- GitHub Actions, Jenkins, GitLab CI, CircleCI — all are tools that implement CI/CD
- A pipeline failing is not a problem — it's CI/CD doing its job

---

### Key Takeaway

CI/CD helps teams:
- integrate code frequently
- catch bugs early
- automate builds and tests
- deploy software safely and quickly

## Without CI/CD, modern software development would be slow, risky, and difficult to scale.
