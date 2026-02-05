# Day 12 – Breather & Revision

### Commands 

#### Environment
- uname -a
- uname
- man <command>
- cat /etc/os-release
- Filesystem sanity
- ls
- mv source destination
- mv file file2
- mkdir /tmp/runbook-demo
- cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -l /tmp/runbook-demo

#### CPU/Memory
- ps -o pid
- ps aux --sort=-%cpu | head -10
- pcpu
- comm -p pid
- free -h
- vm_stat

#### Disk check
- df -h
- du -sh /var/log
- iostat
- vmstat
- dstat

#### Network
- ss-tulpn
- netstat -tulpn
- ping google.com

#### Process Commands
- ps
- top
- pgrep
- service commands
- systemctl status ssh
- systemctl list-units --type=service
- systemctl is-enabled ssh

#### Log Commands
- journalctl -u ssh
- journalctl -u ssh -n 50
- journalctl -u ssh -f
- tail -n 50 /var/log/error.log

#### File creation
- touch notes.txt
- echo "Line 1" > notes.txt
- echo "Line 2" >> notes.txt
- echo "Line 3" | tee -a notes.txt
- cat notes.txt
- head -n 2 notes.txt
- tail -n 2 notes.txt
- ls -lR heist-project/ (list al the files and sub directories)

#### File Transfer
- ssh -i "key.pem" user@publicip (for ssh to any machine)
- sudo apt update (update latest package)
- sudo apt install pkgname (installation of service)
- ssh-keygen (use to generate public key and private key)
- systemctl status service.name (checking status of service installed )
- journalctl -u service.name (check log - use to troubleshoot)
- sudo tail /var/log/error.log (show latest logs generated)
- scp -i key.pem user@publicip:path_of_file (use to download file from server to local system)

#### User and Group Management
- useradd
- userdel
- passwd
- groupadd
- gpasswd
- usermod
- sudo useradd -m username -s /usr/bin/bash
- sudo cat /etc/passwd
- sudo groupadd grpname
- cat /etc/group
- sudo gpasswd -a username groupname
- sudo usermod -aG dev,admin berlin
- sudo chown tokyo devops-file.txt
- sudo chown user:group file/dir
- chmod 775 dir
- ls -l filename
- sudo chown newowner filename
- sudo chgrp newgroup filename
- sudo chown owner:group filename
- sudo chown -R owner:group directory/
- sudo chown :groupname filename

#### File Permission and operations
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

#### Volume Management 
- lsblk
- df -h
- lvm
- pvcreate /dev/nvme1n1 /dev/nvme2n1 /dev/nvme3n1
- pvs
- vgcreate aws1_vg /dev/nvme1n1 /dev/nvme2n1
- vgs
- lvcreate -L 10G -n aws1_lv aws1_vg
- lvs
- pvs
- pvdisolay
- vgdisplay
- mkdir /mnt/aws1_lv_mount
- mkfs.ext4 /dev/aws1_vg/aws1_lv
- mount /dev/aws1_vg/aws1_lv /mnt/aws1_lv_mount/
- df -h
- lsblk
- mkdir /mnt/aws1_disk_mount
- mkfs -t ext4 /dev/nvme3n1
- mount /dev/nvme3n1 /mnt/aws1_disk_mount/
- lvextend -L +5G /dev/aws1_vg/aws1_lv
- unmount /mnt/aws1_lv_mount


## Mini Self-Check

#### 1) Which 3 commands save you the most time right now, and why?
- top (shows systems health in real time)
- df -h (show storage consumption )
- journalctl -u service.name (shows service logs )

#### 2) How do you check if a service is healthy? List the exact 2–3 commands you’d run first.
- systemctl status service.name
- journalctl -u service.name | tail -n 20
- ss -lntup | grep service.name

#### 3) How do you safely change ownership and permissions without breaking access? Give one example command.
- ls -l
- chown owner:group file/dir
- chmod 755 file/dir

#### 4) What will you focus on improving in the next 3 days?
- practice linux commands
- practice linux commands
- practice linux commands
