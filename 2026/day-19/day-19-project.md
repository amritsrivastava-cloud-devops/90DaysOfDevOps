# Day 19 – Shell Scripting Project: Log Rotation, Backup & Crontab

## Challenge Tasks

### Task 1: Log Rotation Script
Create `log_rotate.sh` that:
1. Takes a log directory as an argument (e.g., `/var/log/myapp`)
2. Compresses `.log` files older than 7 days using `gzip`
3. Deletes `.gz` files older than 30 days
4. Prints how many files were compressed and deleted
5. Exits with an error if the directory doesn't exist

<img width="1062" height="244" alt="image" src="https://github.com/user-attachments/assets/cf6b74e6-ebb9-4ba4-8f96-ac5c1cc12935" />
<img width="1452" height="930" alt="image" src="https://github.com/user-attachments/assets/fa61dcc6-e5f1-4471-96e2-9149bd963edf" />
<img width="1960" height="940" alt="image" src="https://github.com/user-attachments/assets/576cfbe7-4ad9-4d09-844c-250095db4cf5" />

---

### Task 2: Server Backup Script
Create `backup.sh` that:
1. Takes a source directory and backup destination as arguments
2. Creates a timestamped `.tar.gz` archive (e.g., `backup-2026-02-08.tar.gz`)
3. Verifies the archive was created successfully
4. Prints archive name and size
5. Deletes backups older than 14 days from the destination
6. Handles errors — exit if source doesn't exist
<img width="1408" height="668" alt="image" src="https://github.com/user-attachments/assets/1f52cf02-7c0b-45c7-83a5-7bf0a75bc0f8" />
<img width="1456" height="758" alt="image" src="https://github.com/user-attachments/assets/6daa99c9-a5f8-4d5c-bd5d-52dad020c091" />
<img width="1886" height="1226" alt="image" src="https://github.com/user-attachments/assets/4d5befac-f858-42e8-b591-0cfadee8c0aa" />

---

### Task 3: Crontab
1. Read: `crontab -l` — what's currently scheduled?
2. Understand cron syntax:
   ```
   * * * * *  command
   │ │ │ │ │
   │ │ │ │ └── Day of week (0-7)
   │ │ │ └──── Month (1-12)
   │ │ └────── Day of month (1-31)
   │ └──────── Hour (0-23)
   └────────── Minute (0-59)
   ```
3. Write cron entries (in your markdown, don't apply if unsure) for:
   - Run `log_rotate.sh` every day at 2 AM
   - Run `backup.sh` every Sunday at 3 AM
   - Run a health check script every 5 minutes
<img width="1450" height="244" alt="image" src="https://github.com/user-attachments/assets/5d4e14c5-9346-4418-8f7c-3a5a61c71eb7" />


---

### Task 4: Combine — Scheduled Maintenance Script
Create `maintenance.sh` that:
1. Calls your log rotation function
2. Calls your backup function
3. Logs all output to `/var/log/maintenance.log` with timestamps
4. Write the cron entry to run it daily at 1 AM
<img width="1394" height="496" alt="image" src="https://github.com/user-attachments/assets/8b4945c8-6083-4455-9e63-a3d2cc7982ab" />

- Using Print 
<img width="1410" height="698" alt="image" src="https://github.com/user-attachments/assets/669bb779-65a4-4074-9645-ac5749d27972" />

- Using function 
<img width="1570" height="1172" alt="image" src="https://github.com/user-attachments/assets/00086a3e-0028-4524-8577-7ebfcdc12aa4" />

---

## Hints
- Compress old files: `find /path -name "*.log" -mtime +7 -exec gzip {} \;`
- Timestamp: `date +%Y-%m-%d`
- Tar: `tar -czf backup.tar.gz /source/dir`
- Cron edit: `crontab -e`
- Log with timestamp: `echo "$(date): message" >> logfile`

---
