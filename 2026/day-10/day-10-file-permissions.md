# Day 10 – File Permissions & File Operations Challenge

### Commands Used
- cat
- touch
- echo "content" >> filename.txt
- vi filename
- vi -R filename (read-only)
- cat filename | tail -n 5
- cat filename | head -n 5
- chmod +x filename (executable for all )
- chmod 755 filename (executable for owner)
- chmod 444 filename (read only for all )
- ./filename.sh (execute the file for output)

### What I Learned
- File permissions directly impact security and execution
- Numeric (chmod 755) and symbolic (chmod +x) modes are both important

## Daily Task 

#### Task 1: Create Files 
- Create empty file devops.txt using touch
- Create notes.txt with some content using cat or echo
- Create script.sh using vim with content: echo "Hello DevOps"
- Verify: ls -l to see permissions

<img width="949" height="618" alt="image" src="https://github.com/user-attachments/assets/562b08d9-387b-40c1-8767-4139afef6c2e" />


#### Task 2: Read Files
- Read notes.txt using cat
- View script.sh in vim read-only mode
- Command: vim -R script.sh
- Display first 5 lines of /etc/passwd using head
- Display last 5 lines of /etc/passwd using tail

<img width="959" height="305" alt="image" src="https://github.com/user-attachments/assets/58b147f7-0fa3-49e1-927f-fa90f34e49ae" />

<img width="979" height="864" alt="image" src="https://github.com/user-attachments/assets/9f7b0817-5d94-4cf9-b98f-258d9ec19363" />

<img width="732" height="192" alt="image" src="https://github.com/user-attachments/assets/5917c628-cccf-424b-a3b8-32904d7e016d" />

<img width="828" height="145" alt="image" src="https://github.com/user-attachments/assets/efee0c64-db79-42e5-95a6-4f78e6b2dd6a" />


#### Task 3: Understand Permissions
- Format: rwxrwxrwx (owner-group-others)
- r = read (4), w = write (2), x = execute (1)
- Check your files: ls -l devops.txt notes.txt script.sh

- Answer: What are current permissions? Who can read/write/execute?
<img width="691" height="131" alt="image" src="https://github.com/user-attachments/assets/c820fa88-6e03-41bd-89c6-5165dbd873cf" />

- owner and group can read write , others can only read .

#### Task 4: Modify Permissions 
- Make script.sh executable → run it with ./script.sh
<img width="504" height="46" alt="image" src="https://github.com/user-attachments/assets/4bfdc986-b814-40f9-9c69-affe8b11dc83" />
<img width="634" height="235" alt="image" src="https://github.com/user-attachments/assets/f22ad6bd-842c-46e4-8b2a-f71ee852f109" />

- Set devops.txt to read-only (remove write for all)
<img width="649" height="147" alt="image" src="https://github.com/user-attachments/assets/50bdf5c3-fcec-4c2d-b11c-c335c912ef10" />

- Set notes.txt to 640 (owner: rw, group: r, others: none)
<img width="655" height="109" alt="image" src="https://github.com/user-attachments/assets/e435636f-0472-4427-999c-d1b46c9a46fe" />

- Create directory project/ with permissions 755
<img width="625" height="115" alt="image" src="https://github.com/user-attachments/assets/42a4572b-d6d5-420b-a204-f18cfe03fd64" />

- Verify: ls -l after each change

#### Task 5: Test Permissions (10 minutes)
- Try writing to a read-only file - what happens?

<img width="973" height="844" alt="image" src="https://github.com/user-attachments/assets/08876241-a446-44ed-8350-aa02cac5853c" />

- Try executing a file without execute permission
<img width="422" height="94" alt="image" src="https://github.com/user-attachments/assets/d4157e08-9a63-47f5-bbe9-3a965493f1e3" />

