# Day 03 – Linux Commands Practice

## Process Management

### View processes
- ps
- ps -ef
- ps aux
- top
- htop

### Find process
- ps -ef | grep <process_name>
- pgrep <process_name>
- pidof <process_name>

### Kill / stop process
- kill <PID>
- kill -9 <PID>
- pkill <process_name>
- killall <process_name>

### Process signals
- kill -l
- kill -STOP <PID>
- kill -CONT <PID>

### Background / foreground
- command &
- jobs
- fg %1
- bg %1

### Resource monitoring
- uptime
- free -h
- vmstat
- watch -n 1 "ps aux | sort -nrk 3 | head"

# Priority management
- nice -n 10 <command>
- renice -5 <PID>

### Process tree
- pstree
- pstree -p

### Debugging
- strace -p <PID>

### Systemd services
- systemctl status <service>
- systemctl start <service>
- systemctl stop <service>
- systemctl restart <service>
- systemctl reload <service>
- journalctl -u <service>

## File System Commands

### List files & directories
- ls
- ls -l
- ls -a
- ls -lh
- ls -R

### Navigation
- pwd
- cd /
- cd ..

### Create files & directories
- touch file.txt
- mkdir dir
- mkdir -p dir/subdir/sub/s/

### Copy
- cp file1 file2
- cp -r dir1 dir2
- cp -p file1 file2

### Move / rename
- mv file1 file2
- mv file dir/

### Delete (use carefully)
- rm file
- rm -f file
- rm -r dir
- rm -rf dir

### View file content
- cat file
- less file
- more file
- head file
- tail file
- tail -f file

### File information
- stat file
- file file
- ls -i

### Search
- find /path -name file.txt
- find / -type f -size +100M
- locate file.txt
- updatedb

### Disk usage
- df -h
- df -Th
- df -i
- du -h
- du -sh dir
- lsblk
- mount
- unmount

### Permissions & ownership
- chmod 755 file
- chmod u+x file
- chown user:group file
- chown -R user:group dir

### Links
- ln file hardlink
- ln -s file symlink

### Archive & compression
- tar -cvf archive.tar dir
- tar -xvf archive.tar
- tar -czvf archive.tar.gz dir
- tar -xzvf archive.tar.gz
- zip archive.zip file
- unzip archive.zip

### Compare files
- diff file1 file2
- cmp file1 file2

### File system check (unmounted FS)
- fsck /dev/sdX

## Network Troubleshooting

### Network info
- ip a
- ip link
- ip addr show
- hostname
- hostname -I

### Connectivity
- ping google.com
- ping -c 4 8.8.8.8

### DNS
- nslookup google.com
- dig google.com
- cat /etc/resolv.conf

### Routing
- ip route
- route -n
- traceroute google.com
- tracepath google.com

### Ports & services
- ss -tulnp
- netstat -tulnp
- lsof -i :80

### Test port connectivity
- nc -zv <host> <port>
- telnet <host> <port>

### Firewall
- iptables -L -n
- iptables -L -n -v
- firewall-cmd --list-all
- ufw status

### Performance
- ifconfig
- ethtool eth0
- mii-tool eth0
- iperf3 -s
- iperf3 -c <server_ip>

### Packet capture
- tcpdump -i eth0
- tcpdump -i eth0 port 80
- tcpdump -nn -i eth0

### ARP / MAC
- arp -a
- ip neigh

### HTTP troubleshooting
- curl http://example.com
- curl -I http://example.com
- wget http://example.com

### Network services
- systemctl status NetworkManager
- systemctl restart NetworkManager
- nmcli device status
