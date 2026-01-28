# View processes
- ps
- ps -ef
- ps aux
- top
- htop

# Find process
- ps -ef | grep <process_name>
- pgrep <process_name>
- pidof <process_name>

# Kill / stop process
- kill <PID>
- kill -9 <PID>
- pkill <process_name>
- killall <process_name>

# Process signals
- kill -l
- kill -STOP <PID>
- kill -CONT <PID>

# Background / foreground
- command &
- jobs
- fg %1
- bg %1

# Resource monitoring
- uptime
- free -h
- vmstat
- watch -n 1 "ps aux | sort -nrk 3 | head"

# Priority management
- nice -n 10 <command>
- renice -5 <PID>

# Process tree
- pstree
- pstree -p

# Debugging
- strace -p <PID>

# Systemd services
- systemctl status <service>
- systemctl start <service>
- systemctl stop <service>
- systemctl restart <service>
- systemctl reload <service>
- journalctl -u <service>
