# Day 47 – Advanced Triggers: PR Events, Cron Schedules & Event-Driven Pipelines

## 📌 Overview

In this lab, I explored advanced GitHub Actions triggers including:

* Pull Request lifecycle events
* PR validation checks
* Scheduled workflows using cron
* Smart triggers using path and branch filters
* Workflow chaining using `workflow_run`
* External triggers using `repository_dispatch`

---

## 🔹 Workflow Files

### 1. PR Lifecycle Workflow (`pr-lifecycle.yml`)

* Triggered on PR events: `opened`, `synchronize`, `reopened`, `closed`
* Prints:

  * Event type
  * PR title
  * PR author
  * Source & target branches
* Runs an additional step only when PR is merged

---

### 2. PR Checks Workflow (`pr-checks.yml`)

Implements real-world PR validations:

#### ✅ File Size Check

* Fails if any file exceeds **1 MB**

#### ✅ Branch Name Check

* Valid patterns:

  * `feature/*`
  * `fix/*`
  * `docs/*`

#### ⚠️ PR Body Check

* Warns if PR description is empty (does not fail pipeline)

---

### 3. Scheduled Workflow (`scheduled-tasks.yml`)

* Runs automatically using cron:

  * Every Monday at 2:30 AM UTC → `30 2 * * 1`
  * Every 6 hours → `0 */6 * * *`
* Also supports manual trigger using `workflow_dispatch`

#### 🔍 Health Check

* Uses `curl` to verify a URL response
* Fails if status code is not `200`

---

## 🔹 Cron Expressions

| Description                          | Cron           |
| ------------------------------------ | -------------- |
| Every weekday at 9 AM IST            | `30 3 * * 1-5` |
| First day of every month at midnight | `0 0 1 * *`    |

---

## 🔹 Smart Triggers

### `paths`

* Workflow runs **only when specific files change**
* Example:

  ```yaml
  paths:
    - 'src/**'
    - 'app/**'
  ```

### `paths-ignore`

* Workflow is skipped if only specified files change
* Example:

  ```yaml
  paths-ignore:
    - '*.md'
    - 'docs/**'
  ```

---

## 🔹 Branch Filters

Used to restrict workflow execution:

```yaml
branches:
  - main
  - 'release/*'
```

---

## 🔹 Workflow Chaining

### `workflow_run`

* Triggers a workflow after another workflow completes
* Example:

  * Run tests → then deploy

### Behavior:

* Runs only after the specified workflow finishes
* Can check result using:

  ```yaml
  github.event.workflow_run.conclusion
  ```

---

## 🔹 workflow_run vs workflow_call

| Feature  | workflow_run             | workflow_call   |
| -------- | ------------------------ | --------------- |
| Purpose  | Chain workflows          | Reuse workflows |
| Trigger  | After workflow completes | Called directly |
| Use Case | CI → CD pipeline         | DRY workflows   |

---

## 🔹 External Triggers (`repository_dispatch`)

* Allows external systems to trigger workflows

### Example Use Cases:

* Slack bot triggers deployment
* Monitoring system detects downtime
* External CI/CD tool initiates pipeline

### Example Payload:

```json
{
  "environment": "production"
}
```

---

## 🔹 Key Learnings

* GitHub Actions supports event-driven automation
* PR checks improve code quality before merging
* Cron jobs enable automated maintenance tasks
* Workflow chaining creates real CI/CD pipelines
* External triggers integrate third-party systems

---

## 📸 Screenshot

*Add screenshot of PR checks running here*

---

## ✅ Conclusion

This exercise helped me understand how to build production-level CI/CD pipelines using advanced GitHub Actions triggers, making workflows smarter, automated, and event-driven.

---

# 🚀 #90DaysOfDevOps #DevOpsKaJosh #TrainWithShubham
