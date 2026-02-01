# Day 09 – Linux User & Group Management Challenge

### Commands Used
- useradd
- userdel
- passwd
- groupadd
- gpasswd
- usermod
- sudo useradd -m username -s /usr/bin/bash
- Command: sudo cat /etc/passwd
- Command: sudo groupadd grpname
- Command: cat /etc/group
- Command: sudo gpasswd -a username groupname
- Command: sudo usermod -aG dev,admin berlin
- Command: sudo chown user:group file/dir
- Command: chmod 775 dir

### Challenges Faced
- Permission denied until group ownership and directory permissions were aligned

### What I Learned
- User and group management is the foundation of system security
- Correct permissions prevent both outages and security issues
- Shared directories work smoothly only when groups are configured properly

## Task 1: Create Users 
- Create three users with home directories and passwords:
- tokyo , berlin , professor
- Command: sudo useradd -m username -s /usr/bin/bash

<img width="668" height="402" alt="image" src="https://github.com/user-attachments/assets/dc55aa17-8338-4cbc-8396-a98ed44b3f03" />

- Verify: Check /etc/passwd and /home/ directory
- Command: sudo cat /etc/passwd
- Command: cd /home

<img width="669" height="920" alt="image" src="https://github.com/user-attachments/assets/62d2a9a1-f371-4cfd-948d-b7bbeeb6be4a" />

## Task 2: Create Groups
- Create two groups:
- developers , admins
- Command: sudo groupadd grpname
- Command: cat /etc/group
<img width="549" height="38" alt="image" src="https://github.com/user-attachments/assets/92f05f37-6ae8-4008-83fa-0058a0e64ec3" />

- Verify: Check /etc/group
<img width="438" height="221" alt="image" src="https://github.com/user-attachments/assets/637e342b-6438-4c8a-a37e-b95135351ea2" />

## Task 3: Assign to Groups
- Assign users:
- tokyo → developers
- berlin → developers + admins (both groups)
- professor → admins
- Verify: Use appropriate command to check group membership
- Command: sudo gpasswd -a username groupname
- Command: sudo usermod -aG dev,admin berlin

<img width="664" height="132" alt="image" src="https://github.com/user-attachments/assets/c8dec1b7-ba85-47a2-8afa-e83d7dbebb2d" />

<img width="406" height="70" alt="image" src="https://github.com/user-attachments/assets/3315f041-0d32-4b6a-b4fa-d73818db7dc0" />

## Task 4: Shared Directory
- Create directory: /opt/dev-project
- Set group owner to developers
- Command: sudo chown user:group file/dir
- Set permissions to 775 (rwxrwxr-x)
- Command: chmod 775 dir
- Test by creating files as tokyo and berlin
- checked - professor can't create anything 
- Verify: Check permissions and test file creation

<img width="664" height="538" alt="image" src="https://github.com/user-attachments/assets/f74dd1fd-a4b3-4f7f-84ae-65f33ca92565" />
<img width="667" height="251" alt="image" src="https://github.com/user-attachments/assets/29168e84-77d9-41c2-b068-096fb6bd453e" />
<img width="624" height="535" alt="image" src="https://github.com/user-attachments/assets/8a515a60-9985-4f80-9da7-9e3bb895de7a" />
<img width="620" height="173" alt="image" src="https://github.com/user-attachments/assets/03f44aae-fdec-4619-a5d8-cbcadeb0524b" />

## Task 5: Team Workspace
- Create user nairobi with home directory
- Create group project-team
- Add nairobi and tokyo to project-team
- Create /opt/team-workspace directory
- Set group to project-team, permissions to 775
- Test by creating file as nairobi

<img width="638" height="140" alt="image" src="https://github.com/user-attachments/assets/15e219c0-003b-4edc-9fd1-7f27207770e2" />
<img width="673" height="453" alt="image" src="https://github.com/user-attachments/assets/b77b8a2c-595d-481c-832f-806101a7d8cb" />
<img width="608" height="193" alt="image" src="https://github.com/user-attachments/assets/1059d84a-b82f-41fe-8ed1-a54ae8990255" />
<img width="603" height="175" alt="image" src="https://github.com/user-attachments/assets/88b8e5e2-3b15-46e2-9167-fa239b5ff00c" />




