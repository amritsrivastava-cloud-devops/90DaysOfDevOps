# Day 38 – YAML Basics

## Challenge Tasks

### Task 1: Key-Value Pairs
Create `person.yaml` that describes yourself with:
- `name`
- `role`
- `experience_years`
- `learning` (a boolean)

**Verify:** Run `cat person.yaml` — does it look clean? No tabs?

```bash
name: Amrit Srivastava

role: Devops Engineer

experience_years: 3

learning: True
```
<img width="1214" height="382" alt="image" src="https://github.com/user-attachments/assets/145e1962-7e75-4ef0-8c61-884d4beadb50" />

- YAML does not allow tabs
- Only spaces should be used for indentation.
---

### Task 2: Lists
Add to `person.yaml`:
- `tools` — a list of 5 DevOps tools you know or are learning
- `hobbies` — a list using the inline format `[item1, item2]`

Write in your notes: What are the two ways to write a list in YAML?
- block style
- inline style

```
name: Amrit Srivastava

role: Devops Engineer

experience_years: 3

learning: True

tools:
  - linux
  - networking
  - git
  - github
  - docker
  - jira

hobbies: [cricket, metaverse, gta, designing, infra-creation, picture-creation]
```
---

### Task 3: Nested Objects
Create `server.yaml` that describes a server:
- `server` with nested keys: `name`, `ip`, `port`
- `database` with nested keys: `host`, `name`, `credentials` (nested further: `user`, `password`)

```
server:
  name: PRODSERVER1
  ip: 192.168.1.21
  port: 80

database:
  host: localhost
  name: app_db
  Credentials:
    - user: admin
    - password: 12345@admin
```
**Verify:** Try adding a tab instead of spaces — what happens when you validate it?
- found character '\t' that cannot start any token (yaml supports only space)
---

### Task 4: Multi-line Strings
In `server.yaml`, add a `startup_script` field using:
1. The `|` block style (preserves newlines)
2. The `>` fold style (folds into one line)

```
server:
  name: PRODSERVER1
  ip: 192.168.1.21
  port: 80

database:
  host: localhost
  name: app_db
  Credentials:
    - user: admin
    - password: 12345@admin
      
startup_script_pipe: |
  #!/bin/bash
  echo "start nginx server"
  systemctl start nginx
  echo "server started"
  
startup_script_fold: >
  #!/bin/bash
  echo "start nginx server"
  systemctl start nginx
  echo "server started"
```
Write in your notes: When would you use `|` vs `>`?
- Difference Between | and >

#### | (Pipe Style)
- Preserves line breaks
- Used for scripts, logs, configs
- Example output:
```
#!/bin/bash
echo "Starting server"
systemctl start nginx
```
#### > (Fold Style)
- Converts new lines into spaces
- Used for long text or messages
- Example output:
```
#!/bin/bash echo "Starting server" systemctl start nginx
```
---

### Task 5: Validate Your YAML
1. Install `yamllint` or use an online validator
2. Validate both your YAML files
3. Intentionally break the indentation — what error do you get?
4. Fix it and validate again

<img width="1636" height="894" alt="image" src="https://github.com/user-attachments/assets/b017c15c-970f-42fc-9050-3f92a10019c7" />
<img width="1618" height="836" alt="image" src="https://github.com/user-attachments/assets/995de9fc-77cc-47aa-8228-3be261f25731" />

---

### Task 6: Spot the Difference
Read both blocks and write what's wrong with the second one:

```yaml
# Block 1 - correct
name: devops
tools:
  - docker
  - kubernetes
```

```yaml
# Block 2 - broken
name: devops
tools:
- docker
  - kubernetes
```
- space is not correct , indentation is not proper for Block2
---

## Hints
- YAML uses **spaces only** — never tabs
- Indentation is everything — 2 spaces is standard
- Strings don't need quotes unless they contain special characters (`:`, `#`, etc.)
- `true`/`false` are booleans, `"true"` is a string
- Validate online: yamllint.com

### Key Learnings
1️⃣ YAML uses spaces only
- Tabs break YAML parsing.
2️⃣ Indentation defines structure
- Even a small indentation mistake can break the entire configuration.
3️⃣ YAML supports powerful structures
- Lists
- Nested objects
- Multi-line strings

## These features make YAML perfect for CI/CD pipelines and infrastructure configuration.
