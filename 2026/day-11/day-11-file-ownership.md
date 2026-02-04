# Day 11 – File Ownership Challenge (chown & chgrp)

## Challenge Tasks

### Task 1: Understanding Ownership 

1. Run `ls -l` in your home directory
2. Identify the **owner** and **group** columns
3. Check who owns your files

<img width="1574" height="556" alt="image" src="https://github.com/user-attachments/assets/225970cf-0cba-44b6-9b22-f562ca380dc9" />

**Format:** `-rw-r--r-- 1 owner group size date filename`

Document: What's the difference between owner and group?

- Owner is user having permission to read write execute file
- Group is set of users who have permission same as group has . ex - if group is developers and tokyo and berlin are members and if group has permission of read write and execute then both member tokyo and berlin can do it .
  
---

### Task 2: Basic chown Operations 

1. Create file `devops-file.txt`
2. Check current owner: `ls -l devops-file.txt`
3. Change owner to `tokyo` (create user if needed)
4. Change owner to `berlin`
5. Verify the changes

<img width="1474" height="898" alt="image" src="https://github.com/user-attachments/assets/4a9c54f2-0b4f-4738-8cbf-97295af3d0e8" />


**Try:**
```bash
sudo chown tokyo devops-file.txt
```
- Note : Using command sudo chown tokyo: devops-file.txt (changed group also to tokyo)
---

### Task 3: Basic chgrp Operations 

1. Create file `team-notes.txt`
2. Check current group: `ls -l team-notes.txt`
3. Create group: `sudo groupadd heist-team`
4. Change file group to `heist-team`
5. Verify the change

<img width="1484" height="754" alt="image" src="https://github.com/user-attachments/assets/e6f3d10b-d499-4956-af77-88814a67f065" />

---

### Task 4: Combined Owner & Group Change 

Using `chown` you can change both owner and group together:

1. Create file `project-config.yaml`
2. Change owner to `professor` AND group to `heist-team` (one command)
3. Create directory `app-logs/`
4. Change its owner to `berlin` and group to `heist-team`

<img width="1484" height="754" alt="image" src="https://github.com/user-attachments/assets/bffd304b-9d53-4509-99dc-8718bb013042" />

<img width="1484" height="754" alt="image" src="https://github.com/user-attachments/assets/d3488691-145d-4541-90f1-76eca5ce0b40" />

**Syntax:** `sudo chown owner:group filename`

---

### Task 5: Recursive Ownership 

1. Create directory structure:
   ```
   mkdir -p heist-project/vault
   mkdir -p heist-project/plans
   touch heist-project/vault/gold.txt
   touch heist-project/plans/strategy.conf
   ```
<img width="1458" height="858" alt="image" src="https://github.com/user-attachments/assets/ac7f9879-d33e-4f99-b5e5-29d4a80dcd75" />
<img width="1342" height="644" alt="image" src="https://github.com/user-attachments/assets/327f25bc-28ce-420b-bd4e-420135be1c8f" />

2. Create group `planners`: `sudo groupadd planners`

3. Change ownership of entire `heist-project/` directory:
   - Owner: `professor`
   - Group: `planners`
   - Use recursive flag (`-R`)

<img width="1456" height="850" alt="image" src="https://github.com/user-attachments/assets/0de6796f-2b2a-4209-84d3-07653122803f" />

4. Verify all files and subdirectories changed: `ls -lR heist-project/`

<img width="1224" height="624" alt="image" src="https://github.com/user-attachments/assets/f2494ae7-385a-48ad-8460-ed9431ade8a8" />

<img width="1410" height="672" alt="image" src="https://github.com/user-attachments/assets/e0cc66c3-caae-45a7-9dec-f998b0de230b" />

---

### Task 6: Practice Challenge 

1. Create users: `tokyo`, `berlin`, `nairobi` (if not already created)
2. Create groups: `vault-team`, `tech-team`

<img width="1296" height="380" alt="image" src="https://github.com/user-attachments/assets/9fb32ed2-b16a-4bd2-980f-d8be87096e05" />

3. Create directory: `bank-heist/`
4. Create 3 files inside:
   ```
   touch bank-heist/access-codes.txt
   touch bank-heist/blueprints.pdf
   touch bank-heist/escape-plan.txt
   ```
<img width="1480" height="650" alt="image" src="https://github.com/user-attachments/assets/1927089c-390e-40c4-84e3-16e948ffd489" />

5. Set different ownership:
   - `access-codes.txt` → owner: `tokyo`, group: `vault-team`
   - `blueprints.pdf` → owner: `berlin`, group: `tech-team`
   - `escape-plan.txt` → owner: `nairobi`, group: `vault-team`

**Verify:** `ls -l bank-heist/`

<img width="1488" height="886" alt="image" src="https://github.com/user-attachments/assets/6314b7ac-50b5-4d51-acff-62f8bad4f78f" />

---

## Key Commands Reference

```bash
# View ownership
ls -l filename

# Change owner only
sudo chown newowner filename

# Change group only
sudo chgrp newgroup filename

# Change both owner and group
sudo chown owner:group filename

# Recursive change (directories)
sudo chown -R owner:group directory/

# Change only group with chown
sudo chown :groupname filename
```

---

## Hints

- Most `chown`/`chgrp` operations need `sudo`
- Use `-R` flag for recursive directory changes
- Always verify with `ls -l` after changes
- User must exist before using in `chown`
- Group must exist before using in `chgrp`/`chown`
