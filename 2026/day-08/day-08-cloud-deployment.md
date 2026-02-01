# Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

### Commands Used
- ssh -i "key.pem" user@publicip (for ssh to any machine)
- sudo apt update (update latest package)
- sudo apt install pkgname (installation of service)
- ssh-keygen (use to generate public key and private key)
- systemctl status service.name (checking status of service installed )
- journalctl -u service.name (check log - use to troubleshoot)
- sudo tail /var/log/error.log (show latest logs generated)
- scp -i key.pem user@publicip:path_of_file (use to download file from server to local system)

### Challenges Faced
- While downloading file to local system with scp i faced issue with correct command , fixed it and its working fine 

### What I Learned
- Cloud servers are useless without correct network and security rules
- SSH and service validation are core daily DevOps tasks
- Logs are the first place to look when something goes wrong

## Part 1: Launch Cloud Instance & SSH Access 
- Step 1: Create a Cloud Instance

<img width="1595" height="400" alt="image" src="https://github.com/user-attachments/assets/a123abfc-b1aa-4e85-8144-20a3dbb2e300" />

- Step 2: Connect via SSH
- Command: ssh -i "key.pem" user@publicip
<img width="821" height="257" alt="image" src="https://github.com/user-attachments/assets/a81ab68d-01dd-4c96-b513-523b136305c5" />
<img width="524" height="514" alt="image" src="https://github.com/user-attachments/assets/64dfed9c-f998-4aa6-94ff-69ff7fb1aa53" />

- Step 3: Connecting another server with ubuntu using ssh-keygen

<img width="1666" height="521" alt="image" src="https://github.com/user-attachments/assets/b46b985d-e33c-43b0-b76b-ccfd4fa3361b" />
<img width="842" height="772" alt="image" src="https://github.com/user-attachments/assets/bfc9fd03-abe1-48cd-865f-c02c60f6bb2c" />

## Part 2: Install Docker & Nginx 
- Step 1: Update System
- Command: sudo apt update 
<img width="839" height="993" alt="image" src="https://github.com/user-attachments/assets/d4caf7ce-077f-4027-9046-d812ae83b17d" />

- Step 2: Install Nginx
- Command: sudo apt install nginx
- Step 3: Verify Nginx is running
- Command: systemctl status nginx

<img width="840" height="942" alt="image" src="https://github.com/user-attachments/assets/d0b5262e-5b22-4b90-9317-ada83931efcf" />

## Part 3: Security Group Configuration 
- Test Web Access: Open browser and visit: http://<your-instance-ip>

<img width="1719" height="817" alt="image" src="https://github.com/user-attachments/assets/b248c78c-fab4-4687-9ab6-f7db63290e98" />

- Changing inbound rule in security group

<img width="1908" height="698" alt="image" src="https://github.com/user-attachments/assets/d1cc3d54-3c72-480c-a13e-a1efd0dac9b3" />

- Checking now

<img width="1744" height="752" alt="image" src="https://github.com/user-attachments/assets/951898d7-a6e3-406e-a68b-8cafb66ca1a6" />

## Part 4: Extract Nginx Logs 
- Step 1: View Nginx Logs
- Command :journalctl -u nginx

 <img width="929" height="135" alt="image" src="https://github.com/user-attachments/assets/f8c388ff-059f-4f7c-ba97-71880c3ba3ba" />

- Check access.log and Error.log in /var/log/nginx
- Command: sudo tail /var/log/nginx/access.log
- Command: sudo tail /var/log/nginx/error.log

<img width="1099" height="214" alt="image" src="https://github.com/user-attachments/assets/ded91d17-bdef-432c-9c33-7ba38136b3d1" />

- Step 2: Save Logs to File
- Command: sudo cat /var/log/nginx/access.log > nginx-logs.txt

<img width="1098" height="266" alt="image" src="https://github.com/user-attachments/assets/4aecca5c-bd1e-4dd3-94d6-bc40470e69fe" />

- Step 3: Download Log File to Your Local Machine
- Command: scp -i linuxpractice1.pem ubuntu@54.242.185.218:/home/ubuntu/nginx-logs.txt .

<img width="1053" height="989" alt="image" src="https://github.com/user-attachments/assets/571b401c-1108-48a3-8bd0-87a0183341eb" />




