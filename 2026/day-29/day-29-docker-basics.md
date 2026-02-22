# Day 29 – Introduction to Docker

## 📌 Goal
Understand what Docker is and run your first container.

Today I learned:
- Why containers exist
- How Docker is different from Virtual Machines
- Docker architecture and core components
- How to run, manage, and explore containers

---

## Task 1: What is Docker?

### What is a Container?
A **container** is a lightweight, portable unit that packages:
- Application code
- Dependencies
- Libraries
- Runtime

Containers run the same way on **any machine**, eliminating the classic  
> “It works on my machine” problem.

They share the host OS kernel, making them **fast, small, and efficient**.

---

### Why Do We Need Containers?
- Consistent environments across dev, test, and prod
- Faster application startup
- Better resource utilization
- Easy scaling and deployment
- Ideal for microservices and CI/CD pipelines

---

### Containers vs Virtual Machines

| Feature | Containers | Virtual Machines |
|------|-----------|----------------|
| OS | Share host OS | Separate OS per VM |
| Size | MBs | GBs |
| Startup | Seconds | Minutes |
| Performance | Near native | Slower |
| Isolation | Process-level | Full OS-level |

- Containers are **lighter and faster**, VMs are **heavier but more isolated**.

---

### Docker Architecture (In My Words)

Docker follows a **client-server architecture**:

- **Docker Client**  
  Used to run Docker commands (`docker run`, `docker ps`, etc.)

- **Docker Daemon (dockerd)**  
  Runs in the background and manages images, containers, networks, and volumes

- **Docker Image**  
  Read-only template used to create containers

- **Docker Container**  
  A running instance of an image

- **Docker Registry**  
  Stores images (example: Docker Hub)

📌 Flow:
Docker Client → Docker Daemon → Image (from Registry) → Container

---

## Task 2: Install Docker

### 🔹 Install Docker
Installed Docker on my machine using official documentation.

### 🔹 Verify Installation
```bash
sudo apt install docker.io
sudo systemctl status docker
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ubuntu && newgrp docker
docker --version
docker info
```

<img width="1901" height="611" alt="image" src="https://github.com/user-attachments/assets/bdec16e0-ce75-480f-96db-66242cc20e39" />
<img width="1313" height="933" alt="image" src="https://github.com/user-attachments/assets/52cabd0c-66e6-4256-ad47-3728280d37ad" />


```
Run First Container
docker run hello-world
```

### Output explained:
- Docker checked for the image locally
- Pulled it from Docker Hub
- Created and ran a container
- Printed a success message

<img width="1751" height="908" alt="image" src="https://github.com/user-attachments/assets/da43c514-1e4c-46ac-9d52-8f2f519cb71e" />

## Task 3: Run Real Containers

### Run Nginx Container
docker run -d -p 80:80 nginx #we can use any port remember portofcontainer:portoflocalos

### Accessed in browser:
👉 http://<publicip>:8080

<img width="1888" height="184" alt="image" src="https://github.com/user-attachments/assets/fee8b0e8-1b4d-40a3-9cae-8c62108f592e" />
<img width="1468" height="532" alt="image" src="https://github.com/user-attachments/assets/7ef619b3-9544-4671-9810-aa94767e943c" />

### Run Ubuntu in Interactive Mode

```
docker run -itd ubuntu
docker exec -it <container-id> bash
```

Explored inside container:
```
ls
cat /etc/os-release
exit
```

<img width="1896" height="806" alt="image" src="https://github.com/user-attachments/assets/633fc909-79c8-48ab-8c9e-76050b228ac7" />

### List Containers

```
docker ps          # Running containers
docker ps -a       # All containers
```

<img width="1902" height="390" alt="image" src="https://github.com/user-attachments/assets/34184848-44f6-40e8-b9bf-a47369875c2a" />

### Stop and Remove Container
```
docker stop <container_id>
docker rm <container_id>
```
<img width="1765" height="550" alt="image" src="https://github.com/user-attachments/assets/0ce5fa85-f0bb-4af9-8764-89b36e1b99b7" />

## Task 4: Explore Docker

### Detached Mode
```
docker run -d nginx
```

- Runs container in background.

### Custom Container Name
```
docker run --name my-nginx -d nginx
```

### Port Mapping
```
docker run -p 9090:80 nginx
```
<img width="1707" height="799" alt="image" src="https://github.com/user-attachments/assets/cf2c22d5-7a19-4aa6-9003-709c11ea3775" />

<img width="1216" height="566" alt="image" src="https://github.com/user-attachments/assets/d5090363-be40-48d6-8a7e-2a65c423decb" />

<img width="882" height="146" alt="image" src="https://github.com/user-attachments/assets/22a498f6-b437-4a74-b580-b5229c25a02d" />


### View Logs
```
docker logs <container_id>
```

### Exec into Running Container
```
docker exec -it <container_id> /bin/bash
```
<img width="1168" height="574" alt="image" src="https://github.com/user-attachments/assets/17eca9ec-f81d-458a-b376-ac54325199ba" />

### Why Docker Matters for DevOps
- Docker is the backbone of:
- CI/CD pipelines
- Kubernetes
- Microservices architecture
- Cloud-native deployments
