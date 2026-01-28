##Linux Troubleshooting Drill: CPU, Memory, and Logs##

Login to machine and check environment basics 
<img width="1693" height="499" alt="image" src="https://github.com/user-attachments/assets/f3f74e97-974d-4326-b5f2-9a1ac619203d" />

Step 1: Pick a Target Service (keep it simple)

- Choose one service that actually exists on your system:
- I am using ssh for this .
# Use command - systemctl status ssh 
<img width="1884" height="506" alt="image" src="https://github.com/user-attachments/assets/e1c8455a-6558-4d62-bc99-d575e69a3645" />

## Target Service
- Service name: ssh
- Description: Secure remote login service
- Service status checked using systemctl

##Filesystem Sanity Check##

<img width="1301" height="478" alt="image" src="https://github.com/user-attachments/assets/9460ab41-4264-4baf-83aa-adddb47df5e8" />
<img width="1234" height="522" alt="image" src="https://github.com/user-attachments/assets/4b92dd04-44be-40e2-972d-2d8b1fe11a0f" />

- File copied sucessfully .

##CPU & Memory Snapshot

Using top for cpu usage check 
<img width="1472" height="500" alt="image" src="https://github.com/user-attachments/assets/5d2eff5f-3163-42d4-8b7c-c9b1a249ad66" />

Using free -h for RAM usage check 
<img width="1320" height="142" alt="image" src="https://github.com/user-attachments/assets/3ee7d799-4efe-4e68-b51f-2cb3e4facaeb" />

##Disk /IO 

Using df -h 
<img width="985" height="305" alt="image" src="https://github.com/user-attachments/assets/cf07349d-e239-4163-a8df-b0897d91f8c9" />

Using du -sh /var/log for checking log 

<img width="1049" height="225" alt="image" src="https://github.com/user-attachments/assets/3c17e7e1-60f6-4336-b36e-3ade6e68e292" />

using iostat 
<img width="1401" height="417" alt="image" src="https://github.com/user-attachments/assets/139cf2c8-a306-455a-8353-8a4b3251ed3d" />

##Network Snapshot##

using netstat -tulpn
<img width="1450" height="351" alt="image" src="https://github.com/user-attachments/assets/ff342a66-6cef-47b0-b895-920423e3449c" />
using ss -tulpn
<img width="1838" height="310" alt="image" src="https://github.com/user-attachments/assets/0f65fce9-d42d-47ae-840f-f4a43ab0ef8e" />
Using ping 
<img width="898" height="242" alt="image" src="https://github.com/user-attachments/assets/4d9219a5-b64c-4a29-8f2f-bc36cdc25c22" />

##Logs Reviewed ##
using this command to review ssh logs
- journalctl -u ssh -n 50
<img width="1877" height="514" alt="image" src="https://github.com/user-attachments/assets/bb5f1c23-9c55-4b83-a90c-3a8d67c5bfca" />

Using command to check authentication log 
tail -n 50 /var/log/auth.log

<img width="1846" height="372" alt="image" src="https://github.com/user-attachments/assets/69255f54-05f0-426a-9658-f78bb4249f16" />










