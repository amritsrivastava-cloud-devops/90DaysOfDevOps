# Day 14 – Networking Fundamentals & Hands-on Checks

## Quick Concepts (write 1–2 bullets each)
#### OSI layers (L1–L7) vs TCP/IP stack (Link, Internet, Transport, Application)

---
- OSI Layer is 7 layers
- Application Layer
- Presentation Layer
- Session Layer
- Transport Layer
- Network Layer
- Data Link Layer
- Physical Layer
---

- TCP /IP
- Application Layer
- Transport Layer
- Internet Layer
- Network Interface

<img width="912" height="436" alt="image" src="https://github.com/user-attachments/assets/38c6f3d0-1add-40ff-bfc3-5814b2727757" />




#### Where **IP**, **TCP/UDP**, **HTTP/HTTPS**, **DNS** sit in the stack
- IP ( Internet Layer)
- TCP/UDP ( Transport Layer )
- Http/Https (Application Layer )
- DNS ( Application Layer )


#### One real example: “`curl https://example.com` = App layer over TCP over IP”
	•	Layer 7 – Application:
	•	curl sends an HTTP request.
	•	DNS lookup happens here (if not cached).
	•	Layer 6 – Presentation:
	•	TLS/SSL encryption (because it’s HTTPS).
	•	Layer 5 – Session:
	•	Session setup and maintenance (conceptual).
	•	Layer 4 – Transport:
	•	TCP establishes a connection (3-way handshake).
	•	Uses destination port 443.
	•	Layer 3 – Network:
	•	IP handles source and destination IP routing.
	•	Layer 2 – Data Link:
	•	Frames created (MAC addressing, ARP if needed).
	•	Layer 1 – Physical:
	•	Bits transmitted over wire/Wi-Fi.

---

## Hands-on Checklist (run these; add 1–2 line observations)
- **Identity:** `hostname -I` (or `ip addr show`) — note your IP.
<img width="1484" height="690" alt="image" src="https://github.com/user-attachments/assets/32d17a48-6e52-481a-bee8-c9f51776ebf0" />

- **Reachability:** `ping <target>` — mention latency and packet loss.
<img width="1390" height="712" alt="image" src="https://github.com/user-attachments/assets/7d06b88a-e8e5-4028-b3e8-7c44bd6469cc" />

- **Path:** `traceroute <target>` (or `tracepath`) — note any long hops/timeouts.
<img width="2608" height="946" alt="image" src="https://github.com/user-attachments/assets/54a44798-3ebf-4a0e-acfb-28f47eb8d9da" />
<img width="2176" height="1280" alt="image" src="https://github.com/user-attachments/assets/4e627256-47a9-45f3-8be7-845dad186727" />

- **Ports:** `ss -tulpn` (or `netstat -tulpn`) — list one listening service and its port.
<img width="2836" height="416" alt="image" src="https://github.com/user-attachments/assets/9e642658-88be-46c9-9eba-d15fb5bc7df9" />
<img width="2836" height="416" alt="image" src="https://github.com/user-attachments/assets/cd717f10-ba54-4254-9e7a-614b870fae63" />

- **Name resolution:** `dig <domain>` or `nslookup <domain>` — record the resolved IP.
<img width="1748" height="914" alt="image" src="https://github.com/user-attachments/assets/962e14cd-efc4-4ce7-86b4-46d74e2f9e46" />
<img width="1766" height="526" alt="image" src="https://github.com/user-attachments/assets/90a564ae-a0f9-4d02-b710-f9d9bda3148b" />


- **HTTP check:** `curl -I <http/https-url>` — note the HTTP status code.
<img width="2940" height="570" alt="image" src="https://github.com/user-attachments/assets/5502f778-f3e6-46d0-9526-152a30520064" />

- **Connections snapshot:** `netstat -an | head` — count ESTABLISHED vs LISTEN (rough).
<img width="1660" height="438" alt="image" src="https://github.com/user-attachments/assets/9ee6bba5-b80b-445b-95a1-0fc25ae19090" />

Pick one target service/host (e.g., `google.com`, your lab server, or a local service) and stick to it for ping/traceroute/curl where possible.

---

## Mini Task: Port Probe & Interpret
1) Identify one listening port from `ss -tulpn` (e.g., SSH on 22 or a local web app).
<img width="1336" height="162" alt="image" src="https://github.com/user-attachments/assets/b7299128-ad45-4b85-8702-69c2851fbc80" />

3) From the same machine, test it: `nc -zv localhost <port>` (or `curl -I http://localhost:<port>`).
<img width="1066" height="198" alt="image" src="https://github.com/user-attachments/assets/9dadb42f-df37-4049-9b06-b51980257d64" />

5) Write one line: is it reachable? If not, what’s the next check? (e.g., service status, firewall).
- Reachable
- we can check ufw status if not reachable . ufw status command .
---

## Reflection (add to your markdown)
- Which command gives you the fastest signal when something is broken?
- Ping

- What layer (OSI/TCP-IP) would you inspect next if DNS fails? If HTTP 500 shows up?
- Application layer -> Transport Layer
- HTTP 500 = server/app error first, not network

- Follow-up checks you’d run in a real incident.
- sytemctl status firewalld
- journalctl -u firewalld
- cat /etc/resolv.conf
- ufw status
- ping

---
