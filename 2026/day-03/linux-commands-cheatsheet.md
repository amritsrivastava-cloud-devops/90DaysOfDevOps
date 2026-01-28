📌 Process Management
View Processes

ps

ps -ef

ps aux

top

htop

Find Process

ps -ef | grep <process_name>

pgrep <process_name>

pidof <process_name>

Kill / Stop Process

kill <PID>

kill -9 <PID>

pkill <process_name>

killall <process_name>

Process Signals

kill -l

kill -STOP <PID>

kill -CONT <PID>

Background / Foreground

command &

jobs

fg %1

bg %1

Resource Monitoring

uptime

free -h

vmstat

watch -n 1 "ps aux | sort -nrk 3 | head"

Priority Management

nice -n 10 <command>

renice -5 <PID>

Process Tree

pstree

pstree -p

Debugging

strace -p <PID>

Systemd Services

systemctl status <service>

systemctl start <service>

systemctl stop <service>

systemctl restart <service>

systemctl reload <service>

journalctl -u <service>
