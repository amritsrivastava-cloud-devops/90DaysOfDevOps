# Day 42 – Runners: GitHub-Hosted & Self-Hosted

## Challenge Tasks

### Task 1: GitHub-Hosted Runners
1. Create a workflow with 3 jobs, each on a different OS:
   - `ubuntu-latest`
   - `windows-latest`
   - `macos-latest`
2. In each job, print:
   - The OS name
   - The runner's hostname
   - The current user running the job
3. Watch all 3 run in parallel

Write in your notes: What is a GitHub-hosted runner? Who manages it?

<img width="1857" height="731" alt="image" src="https://github.com/user-attachments/assets/71cecb34-ca8c-43d1-970a-24f8c94a72fe" />

```
name: Different-OS

on:
 workflow_dispatch:

jobs:
  TEST1LINUX:
    runs-on: ubuntu-latest
    steps:
      - name: os name 
        run: uname -a
      - name: runner hostname
        run: hostname
      - name: current user
        run: whoami

  TEST2WINDOWS:
    runs-on: windows-latest
    steps:
      - name: os name 
        run: systeminfo | findstr /B /C:"OS Name"
      - name: runner hostname
        run: hostname
      - name: current user
        run: whoami

  TEST3MACOS:
    runs-on: macos-latest
    steps:
      - name: os name
        run: sw_vers
      - name: runner hostname
        run: hostname
      - name: current user
        run: whoami
```
---

### Task 2: Explore What's Pre-installed
1. On the `ubuntu-latest` runner, run a step that prints:
   - Docker version
   - Python version
   - Node version
   - Git version

<img width="1877" height="905" alt="image" src="https://github.com/user-attachments/assets/7c823b8a-d781-43e3-bacb-119b3e7baf9b" />

```
name: Different-OS

on:
 workflow_dispatch:

jobs:
  TEST1LINUX:
    runs-on: ubuntu-latest
    steps:
      - name: os name 
        run: uname -a
      - name: runner hostname
        run: hostname
      - name: current user
        run: whoami
      - name: docker vesion
        run: docker --version
      - name: python version
        run: python --version
      - name: node version check
        run: node --version
      - name: git version check
        run: git --version
```

2. Look up the GitHub docs for the full list of pre-installed software on `ubuntu-latest`

Write in your notes: Why does it matter that runners come with tools pre-installed?

Notes Answer

- What is a GitHub-hosted runner?
  - A GitHub-hosted runner is a virtual machine provided and managed by GitHub that runs your workflow jobs.

- Who manages it?
  - GitHub manages:
  - Infrastructure
  - OS updates
  - Installed tools
  - Security patches

- Why Pre-installed Tools Matter
  - Because:
  - Pipelines run faster
  - No need to install basic tools every run
  - Saves build time
  - Reduces workflow complexity
  - Example: Docker, Node, Python, Java already installed.
---

### Task 3: Set Up a Self-Hosted Runner
1. Go to your GitHub repo → Settings → Actions → Runners → **New self-hosted runner**
2. Choose Linux as the OS
3. Follow the instructions to download and configure the runner on:
   - Your local machine, OR
   - A cloud VM (EC2, Utho, or any VPS)
4. Start the runner — verify it shows as **Idle** in GitHub

**Verify:** Your runner appears in the Runners list with a green dot.
```

Download
# Create a folder
$ mkdir actions-runner && cd actions-runner# Download the latest runner package
$ curl -o actions-runner-linux-x64-2.332.0.tar.gz -L https://github.com/actions/runner/releases/download/v2.332.0/actions-runner-linux-x64-2.332.0.tar.gz# Optional: Validate the hash
$ echo "f2094522a6b9afeab07ffb586d1eb3f190b6457074282796c497ce7dce9e0f2a  actions-runner-linux-x64-2.332.0.tar.gz" | shasum -a 256 -c# Extract the installer
$ tar xzf ./actions-runner-linux-x64-2.332.0.tar.gz
Configure
# Create the runner and start the configuration experience
$ ./config.sh --url https://github.com/amritsrivastava-cloud-devops/github-actions-zero-to-hero --token AMEWXQEOXYG5MK23A4OJUFDJWLC76# Last step, run it!
$ ./run.sh
Using your self-hosted runner
# Use this YAML in your workflow file for each job
runs-on: self-hosted
```

<img width="1293" height="537" alt="image" src="https://github.com/user-attachments/assets/e5afe85c-7a1d-48b1-b2a1-938cd485213f" />
<img width="1261" height="666" alt="image" src="https://github.com/user-attachments/assets/ea85a529-aebf-4a25-abc7-00e5dcdd0970" />

---

### Task 4: Use Your Self-Hosted Runner
1. Create `.github/workflows/self-hosted.yml`
2. Set `runs-on: self-hosted`
3. Add steps that:
   - Print the hostname of the machine (it should be YOUR machine/VM)
   - Print the working directory
   - Create a file and verify it exists on your machine after the run
4. Trigger it and watch it run on your own hardware

**Verify:** Check your machine — is the file there?
```

name: Self Hosted

on:
  workflow_dispatch: 


jobs:
  testself-hosted-runner:
    runs-on: self-hosted
    steps:
       - name: hostname of machine
         run: hostname
       - name: working directory
         run: pwd
       - name: create a file and verify
         run: echo "this is for testing purpose " >> test.txt
       - name: verify the file
         run: ls -la

```

<img width="1879" height="907" alt="image" src="https://github.com/user-attachments/assets/ddf67e3b-64cb-452c-8bd5-e1c4e63f8657" />

---

### Task 5: Labels
1. Add a **label** to your self-hosted runner (e.g., `my-linux-runner`)
2. Update your workflow to use `runs-on: [self-hosted, my-linux-runner]`
3. Trigger it — does it still pick up the job?

Write in your notes: Why are labels useful when you have multiple self-hosted runners?

```
Add label in:
Repo → Settings → Actions → Runners → Your Runner

Example label:
my-linux-runner

Update workflow:
runs-on: [self-hosted, my-linux-runner]

Example:
jobs:
  run-on-my-machine:

    runs-on: [self-hosted, my-linux-runner]

    steps:
      - run: hostname
Why Labels Are Useful
Labels help when you have multiple self-hosted runners.

Example:
Runner	Label
GPU machine	gpu
Docker server	docker
High RAM server	high-memory
Then workflow can target:
runs-on: [self-hosted, gpu

```
---

### Task 6: GitHub-Hosted vs Self-Hosted
Fill this in your notes:

|                     | GitHub-Hosted           | Self-Hosted                       |
| ------------------- | ----------------------- | --------------------------------- |
| Who manages it?     | GitHub                  | You                               |
| Cost                | Free with limits        | You pay for server                |
| Pre-installed tools | Many tools installed    | You install manually              |
| Good for            | Normal CI/CD            | Custom environments, heavy builds |
| Security concern    | GitHub manages security | You must secure machine           |

---

## Hints
- Runner setup script is generated by GitHub — just copy and run it
- Self-hosted runner runs as a background service: `./run.sh`
- To run as a service (persistent): `sudo ./svc.sh install && sudo ./svc.sh start`
- `runs-on: self-hosted` targets any self-hosted runner
- `runs-on: [self-hosted, linux, my-label]` targets specific ones
