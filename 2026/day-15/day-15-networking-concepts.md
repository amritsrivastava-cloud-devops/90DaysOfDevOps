# Day 15 – Networking Concepts: DNS, IP, Subnets & Ports

## Task 1: DNS – How Names Become IPs

### 1. What happens when you type `google.com` in a browser?
- When you type google.com, the Application layer performs DNS resolution to convert the domain name into an IP address.
- The Transport layer establishes a connection — DNS uses UDP, and the browser uses TCP (3-way handshake) for reliable communication.
- The Internet layer adds source and destination IP addresses and routes packets across networks to reach Google’s server.
- The Network Access layer converts packets into frames, resolves MAC addresses using ARP, and sends data over Ethernet or Wi-Fi.
- Google’s server responds with webpage data, which travels back through the same TCP/IP layers and is rendered by the browser.

### 2. DNS Record Types
- **A** – Maps a domain name to an IPv4 address  
- **AAAA** – Maps a domain name to an IPv6 address  
- **CNAME** – Alias of one domain pointing to another domain  
- **MX** – Mail exchange record, defines mail servers for a domain  
- **NS** – Specifies authoritative name servers for the domain  

### 3. `dig google.com`

<img width="1077" height="629" alt="image" src="https://github.com/user-attachments/assets/8526b724-b52b-447d-bc8e-773f19da84b0" />

## Task 2: IP Addressing

### 1. What is an IPv4 address?
- An IPv4 address is a 32-bit numeric identifier used to identify devices on a network.
- It is written in dotted decimal format like 192.168.1.10, divided into network and host parts.

### 2. Public vs Private IP
- Public IP – Routable on the internet (Example: 8.8.8.8)
- Private IP – Used within internal networks (Example: 192.168.1.10)

### 3. Private IP Ranges
- 10.0.0.0 – 10.255.255.255
- 172.16.0.0 – 172.31.255.255
- 192.168.0.0 – 192.168.255.255

### 4. ip addr show
- Private ip =172.31.6.109
<img width="1256" height="297" alt="image" src="https://github.com/user-attachments/assets/2d2125df-56d3-4172-b042-a5298deeeca8" />

## Task 3: CIDR & Subnetting

### 1. What does /24 mean?
- /24 means the first 24 bits are used for the network portion, leaving 8 bits for hosts.

### 2. Usable Hosts
- /24 → 256 total, 254 usable
- /16 → 65,536 total, 65,534 usable
- /28 → 16 total, 14 usable

### 3. Why do we subnet?
- Subnetting helps in efficient IP usage, improves security, reduces broadcast traffic, and enables better network organization.

### 4. Quick exercise — fill in:

| CIDR | Subnet Mask     | Total IPs | Usable Hosts |
| ---: | --------------- | --------: | -----------: |
|  /24 | 255.255.255.0   |       256 |          254 |
|  /16 | 255.255.0.0     |    65,536 |       65,534 |
|  /28 | 255.255.255.240 |        16 |           14 |

## Task 4: Ports – The Doors to Services

### 1. What is a port? Why do we need them?
- A port is a logical communication endpoint that allows multiple services to run on the same IP address.

### 2. Document these common ports:

|  Port | Service |
| ----: | ------- |
|    22 | SSH     |
|    80 | HTTP    |
|   443 | HTTPS   |
|    53 | DNS     |
|  3306 | MySQL   |
|  6379 | Redis   |
| 27017 | MongoDB |

### 3. Run `ss -tulpn` — match at least 2 listening ports to their services

<img width="1503" height="368" alt="image" src="https://github.com/user-attachments/assets/3d204bf6-d6bc-4d66-955b-133238f760af" />

## Task 5: Putting It Together
### 1. curl http://myapp.com:8080
- DNS resolves myapp.com to an IP address.
- The request connects to port 8080 over TCP using HTTP protocol.

### 2. App can’t reach DB 10.0.1.50:3306
- Check network connectivity, security groups/firewall rules, correct IP/port, and whether MySQL is listening on port 3306.

## What I Learned (Key Takeaways)
- DNS is the backbone that translates human-readable names into IP addresses.
- Subnetting helps manage networks efficiently and securely.
- Ports allow multiple applications to communicate on the same server without conflict.
