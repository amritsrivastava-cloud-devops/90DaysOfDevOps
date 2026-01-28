You will create a cheat sheet of commands focused on:

- Process management
# ===============================
# LINUX PROCESS MANAGEMENT COMMANDS
# ===============================

# View processes
ps
ps -ef
ps aux
top
htop

# Find process
ps -ef | grep <process_name>
pgrep <process_name>
pidof <process_name>

# Kill / stop process
kill <PID>
kill -9 <PID>
pkill <process_name>
killall <process_name>

# Process signals
kill -l
kill -STOP <PID>
kill -CONT <PID>

# Background / foreground jobs
command &
jobs
fg %1
bg %1
Ctrl + Z

# Resource monitoring
uptime
free -h
vmstat
watch -n 1 "ps aux | sort -nrk 3 | head"

# Process priority
nice -n 10 <command>
renice -5 <PID>

# Process tree
pstree
pstree -p

# CPU / Memory specific
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head
mpstat
iostat

# Run after logout
nohup <command> &
disown

# Debugging
strace -p <PID>

# Systemd service management
systemctl status <service>
systemctl start <service>
systemctl stop <service>
systemctl restart <service>
systemctl reload <service>

# Logs
journalctl -u <service>

# ===============================
# END
# ===============================

- File system

# ==================================
# LINUX FILE SYSTEM COMMANDS
# ==================================

# List files & directories
ls
ls -l
ls -a
ls -lh
ls -R

# Directory navigation
pwd
cd /
cd ..
cd ~
cd -

# Create files & directories
touch file.txt
mkdir dir
mkdir -p dir/subdir

# Copy files & directories
cp file1 file2
cp -r dir1 dir2
cp -p file1 file2

# Move / rename files
mv file1 file2
mv file dir/

# Remove files & directories
rm file
rm -f file
rm -r dir
rm -rf dir

# View file content
cat file
less file
more file
head file
tail file
tail -f file

# File information
stat file
file file
ls -i

# Search files
find /path -name file.txt
find / -type f -size +100M
locate file.txt
updatedb

# Disk usage & space
df -h
du -h
du -sh dir
lsblk
mount
umount

# File permissions
chmod 755 file
chmod u+x file
chown user:group file
chown -R user:group dir

# Symbolic & hard links
ln file hardlink
ln -s file symlink

# Archive & compression
tar -cvf archive.tar dir
tar -xvf archive.tar
tar -czvf archive.tar.gz dir
tar -xzvf archive.tar.gz
zip archive.zip file
unzip archive.zip

# Compare files
diff file1 file2
cmp file1 file2

# File system check
mount | grep "^/"
df -Th
fsck /dev/sdX

# Inode usage
df -i

# ==================================
# END
# ==================================


- Networking troubleshooting

# ==================================
# LINUX NETWORK TROUBLESHOOTING COMMANDS
# ==================================

# Basic network info
ip a
ip link
ip addr show
hostname
hostname -I

# Connectivity check
ping google.com
ping -c 4 8.8.8.8

# DNS troubleshooting
nslookup google.com
dig google.com
cat /etc/resolv.conf

# Routing & gateway
ip route
route -n
traceroute google.com
tracepath google.com

# Listening ports & services
ss -tulnp
netstat -tulnp
lsof -i :80

# Test port connectivity
nc -zv <host> <port>
telnet <host> <port>

# Firewall checks
iptables -L -n
iptables -L -n -v
firewall-cmd --list-all
ufw status

# Network performance
ifconfig
ethtool eth0
mii-tool eth0
iperf3 -s
iperf3 -c <server_ip>

# Packet capture
tcpdump -i eth0
tcpdump -i eth0 port 80
tcpdump -nn -i eth0

# ARP / MAC
arp -a
ip neigh

# HTTP / Proxy test
curl http://example.com
curl -I http://example.com
wget http://example.com

# Network services
systemctl status NetworkManager
systemctl restart NetworkManager
nmcli device status

# ==================================
# END
# ==================================

- This is the command toolkit you will reuse for years.
