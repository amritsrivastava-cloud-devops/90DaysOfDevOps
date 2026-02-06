# NFS & Samba Setup on Ubuntu (Step-by-Step)

This document explains **how to configure NFS and Samba on one Ubuntu server and access them from another Ubuntu server and macOS**. It is written in a **GitHub-ready, interview-oriented** format based on real troubleshooting.

---

## 🏗️ Architecture Used

* **Server A**: Ubuntu (NFS + Samba Server)
* **Server B**: Ubuntu (NFS Client)
* **Client**: macOS (Samba Client)
* **Environment**: AWS EC2

---

## 🔹 Part 1: NFS Configuration (Ubuntu ↔ Ubuntu)

### Step 1: Install NFS packages

**On Server A (NFS Server):**

```bash
sudo apt update
sudo apt install nfs-kernel-server -y
```

**On Server B (NFS Client):**

```bash
sudo apt update
sudo apt install nfs-common -y
```

---

### Step 2: Create NFS shared directory (Server A)

```bash
sudo mkdir -p /srv/nfs-share
sudo chown -R nobody:nogroup /srv/nfs-share
sudo chmod -R 777 /srv/nfs-share
```

---

### Step 3: Configure exports (Server A)

Edit exports file:

```bash
sudo nano /etc/exports
```

Add:

```text
/srv/nfs-share SERVER_B_IP(rw,sync,no_subtree_check)
```

Apply exports:

```bash
sudo exportfs -ra
exportfs -v
```

---

### Step 4: Start & verify NFS service (Server A)

```bash
sudo systemctl start nfs-kernel-server
sudo systemctl enable nfs-kernel-server
sudo systemctl status nfs-kernel-server
```

---

### Step 5: Open firewall & AWS Security Group (CRITICAL)

**Ubuntu (UFW):**

```bash
sudo ufw allow nfs
sudo ufw reload
```

**AWS Security Group (Inbound):**

* TCP **2049** allowed from client IP / subnet

---

### Step 6: Validate export from client (Server B)

```bash
showmount -e SERVER_A_IP
```

---

### Step 7: Mount NFS share (Server B)

```bash
sudo mkdir -p /mnt/nfs
sudo mount SERVER_A_IP:/srv/nfs-share /mnt/nfs
```

If mount hangs, use safe options:

```bash
sudo mount -o soft,timeo=30,retrans=3 SERVER_A_IP:/srv/nfs-share /mnt/nfs
```

Verify:

```bash
df -h
lsblk
```

---

## 🔹 Part 2: Samba Configuration (Ubuntu ↔ macOS)

### Step 1: Install Samba (Server A)

```bash
sudo apt install samba -y
```

---

### Step 2: Create Samba shared directory

```bash
sudo mkdir -p /srv/samba-share
sudo chmod -R 777 /srv/samba-share
```

---

### Step 3: Create Samba user

```bash
sudo useradd sambauser
sudo smbpasswd -a sambauser
sudo smbpasswd -e sambauser
```

> Note: Samba uses its own password database, not Linux passwords.

---

### Step 4: Configure Samba share

Edit config:

```bash
sudo nano /etc/samba/smb.conf
```

Add at the bottom:

```ini
[sambashare]
   path = /srv/samba-share
   browseable = yes
   read only = no
   writable = yes
   guest ok = no
   valid users = sambauser
```

Restart Samba:

```bash
sudo systemctl restart smbd
sudo systemctl status smbd
```

---

### Step 5: Open firewall & AWS Security Group

**Ubuntu (UFW):**

```bash
sudo ufw allow samba
sudo ufw reload
```

**AWS Security Group (Inbound):**

* TCP **445**
* TCP **139**

---

### Step 6: Access Samba from macOS

#### Option A: Finder (Recommended)

1. Open **Finder**
2. Go → **Connect to Server**
3. Enter:

```
smb://SERVER_A_PUBLIC_IP/sambashare
```

4. Login as:

* Username: `sambauser`
* Password: Samba password

---

#### Option B: macOS Terminal

```bash
mkdir ~/samba-test
mount_smbfs //sambauser@SERVER_A_PUBLIC_IP/sambashare ~/samba-test
```

---

## 🔹 Part 3: Persistence using /etc/fstab

### NFS entry example

```text
SERVER_A_IP:/srv/nfs-share  /mnt/nfs  nfs  defaults,_netdev  0  0
```

### Samba entry example

```text
//SERVER_A_IP/sambashare  /mnt/samba  cifs  username=sambauser,password=PASSWORD,_netdev  0  0
```

Test before reboot:

```bash
sudo mount -a
```

---

## ⚠️ Common Issues Faced & Fixes

* **NFS mount hanging** → Port 2049 blocked in AWS SG
* **Server stuck on mount** → Missing `_netdev`
* **Samba auth failure** → Samba password not set
* **Ping works but mount fails** → SG ≠ UFW

---

## 🎯 Interview Takeaway

> NFS is ideal for Linux-to-Linux file sharing, while Samba is used for cross-platform access. Proper firewall rules, AWS Security Groups, and safe fstab options are critical to avoid mount and boot issues.

---

## ✅ Commands Used Summary

* `mount`, `umount`, `df -h`, `lsblk`
* `exportfs`, `showmount`
* `smbpasswd`, `smbclient`
* `systemctl`, `ufw`
* `/etc/exports`, `/etc/samba/smb.conf`, `/etc/fstab`

---

**Author:** Amrit Srivastava
