# Create a EC2 server on AWS free tier account 
<img width="2480" height="1182" alt="image" src="https://github.com/user-attachments/assets/2235a23e-bd7e-4afa-abe5-7b6cfd0901f5" />

# Now connect EC2 machine using connect button on top or either use .pem key to connect 
- I am using terminal to connect to machine
- Note - When ever you shoutdown your ec2 machine your ip will change as you have not selected elastic ip .
- Before using terminal make sure pem key is having permission
- chmod 400 "Linuxfordevops.pem"
- Use command
- ssh -i "Linuxfordevops.pem" ubuntu@ec2-3-228-22-208.compute-1.amazonaws.com
- 
#Enter commands correctly
<img width="1474" height="942" alt="image" src="https://github.com/user-attachments/assets/9af336b9-f2a5-4033-bb62-ea4451eff842" />

#Connected to Ubuntu machine 
<img width="1474" height="942" alt="image" src="https://github.com/user-attachments/assets/58d9feff-78e1-4ad7-ad20-edcb9ba7250e" />

#Using commands uname, hostname , ip addr 
<img width="1468" height="790" alt="image" src="https://github.com/user-attachments/assets/499890cb-6cb5-477f-b365-840b2fc4be5b" />

#Practicing some linux basic commands 
<img width="1308" height="740" alt="Screenshot 2026-01-28 at 12 27 52 PM" src="https://github.com/user-attachments/assets/f862b779-e6f4-4290-be38-bce512187410" />

<img width="1994" height="948" alt="image" src="https://github.com/user-attachments/assets/15749dfb-1c53-47ef-9596-8390df4ea410" />

#Check Running process 
ps aux 
<img width="2104" height="1182" alt="image" src="https://github.com/user-attachments/assets/e3b42b4b-6b82-4563-8b84-d33745845cf6" />

top
<img width="2310" height="1326" alt="image" src="https://github.com/user-attachments/assets/e7ed55d1-733e-4a66-987a-57aff091fdf0" />

#checking service status 
systemctl status ssh 
<img width="2926" height="1152" alt="image" src="https://github.com/user-attachments/assets/5c7cb129-b13b-4db2-ae40-c8b36a602bfe" />

#checking logs
journalctl -u ssh
<img width="2926" height="464" alt="image" src="https://github.com/user-attachments/assets/6fb7f4c4-6eb6-441a-ae8b-9c5080c9c4fe" />











