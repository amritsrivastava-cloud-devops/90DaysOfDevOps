# Day 10 – File Permissions & File Operations Challenge

### Commands Used
### Challenges Faced
### What I Learned

#### Task 1: Create Files 
- Create empty file devops.txt using touch
- Create notes.txt with some content using cat or echo
- Create script.sh using vim with content: echo "Hello DevOps"
- Verify: ls -l to see permissions

#### Task 2: Read Files
- Read notes.txt using cat
- View script.sh in vim read-only mode
- Display first 5 lines of /etc/passwd using head
- Display last 5 lines of /etc/passwd using tail

#### Task 3: Understand Permissions
- Format: rwxrwxrwx (owner-group-others)
- r = read (4), w = write (2), x = execute (1)
- Check your files: ls -l devops.txt notes.txt script.sh

- Answer: What are current permissions? Who can read/write/execute?

#### Task 4: Modify Permissions 
- Make script.sh executable → run it with ./script.sh
- Set devops.txt to read-only (remove write for all)
- Set notes.txt to 640 (owner: rw, group: r, others: none)
- Create directory project/ with permissions 755
- Verify: ls -l after each change

#### Task 5: Test Permissions (10 minutes)
- Try writing to a read-only file - what happens?
- Try executing a file without execute permission
- Document the error messages
