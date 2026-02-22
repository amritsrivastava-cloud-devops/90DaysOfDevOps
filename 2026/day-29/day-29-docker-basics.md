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

## 🛠 Task 2: Install Docker

### 🔹 Install Docker
Installed Docker on my machine using official documentation.

### 🔹 Verify Installation
```bash
sudo apt install docker.io
sudo systemctl status docker
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

### 📖 Output explained:
Docker checked for the image locally
Pulled it from Docker Hub
Created and ran a container
Printed a success message

<img width="1751" height="908" alt="image" src="https://github.com/user-attachments/assets/da43c514-1e4c-46ac-9d52-8f2f519cb71e" />

