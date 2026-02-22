## Docker Concepts
Why, what, and how do we learn Docker?
Virtualization vs Containerisation
Terminologies – Docker Engine, Docker Client, Docker Daemon, Docker Registry, Docker CLI, Docker Desktop, Docker Hub
Containers – Nginx, MySQL, MongoDB, ubuntu
Images - Can be pulled by DockerHub (official images only) + Can be created with Dockerfile
Dockerfile – Step-by-Step Process – Cake example (Blueprint) 
Examples – custom nginx, FastAPI python project, Simple Java Example (Hello Dosto)

## Installation of mysql on docker 

```
docker run -d --name mysql-TWS -e MYSQL_ROOT_PASSWORD=12345 mysql
docker exec -it id bash
mysql -u root -p
```

## Installation of mongodb on docker 

```
docker run -d mongo
docker exec -it id bash
mongosh
```

---

# Creating Dockerfile 
git clone repo
grep -i -r "Welcome to nginx!" /

```Dockerfile
# Take patilla

FROM nginx

# cooker

WORKDIR /app

# ingredients ( local docker )
COPY index.html /usr/share/gninx/html

EXPOSE 80
```

# 🐳 Docker Flags Cheat Sheet

A quick reference for the most commonly used Docker flags.  
Useful for **daily DevOps work, interviews, and CI/CD pipelines**.

---

## 🚀 docker run – Core Flags

| Flag | Description | Example |
|-----|------------|---------|
| `-it` | Interactive terminal | `docker run -it ubuntu` |
| `-d` | Run container in background | `docker run -d nginx` |
| `--rm` | Auto-remove container on exit | `docker run --rm ubuntu` |
| `--name` | Assign custom name | `docker run --name myapp nginx` |

---

## 🌐 Networking & Ports

| Flag | Description | Example |
|-----|------------|---------|
| `-p host:container` | Port mapping | `docker run -p 8080:80 nginx` |
| `--network` | Specify Docker network | `docker run --network mynet nginx` |
| `--hostname` | Set container hostname | `docker run --hostname web1 nginx` |

---

## 📦 Volumes & Storage

| Flag | Description | Example |
|-----|------------|---------|
| `-v host:container` | Mount volume | `docker run -v /data:/app ubuntu` |
| `--mount` | Advanced volume mount | `docker run --mount type=bind,src=/data,dst=/app ubuntu` |
| `--read-only` | Read-only filesystem | `docker run --read-only ubuntu` |

---

## 🔧 Environment & Configuration

| Flag | Description | Example |
|-----|------------|---------|
| `-e` | Set environment variable | `docker run -e ENV=prod ubuntu` |
| `--env-file` | Load env variables from file | `docker run --env-file .env ubuntu` |
| `--workdir` | Set working directory | `docker run --workdir /app ubuntu` |

---

## ⚙️ Resource Management

| Flag | Description | Example |
|-----|------------|---------|
| `--memory` | Limit memory usage | `docker run --memory=512m ubuntu` |
| `--cpus` | Limit CPU usage | `docker run --cpus=1 ubuntu` |
| `--pids-limit` | Limit number of processes | `docker run --pids-limit=100 ubuntu` |

---

## 📥 docker pull Flags

| Flag | Description | Example |
|-----|------------|---------|
| `--all-tags` | Pull all image tags | `docker pull --all-tags ubuntu` |
| `--platform` | Specify OS/architecture | `docker pull --platform linux/amd64 nginx` |

---

## 📋 docker ps Flags

| Flag | Description | Example |
|-----|------------|---------|
| `-a` | Show all containers | `docker ps -a` |
| `-q` | Show only container IDs | `docker ps -q` |
| `--filter` | Filter output | `docker ps --filter status=running` |

---

## 🛑 Stop & Remove

| Command | Flag | Description | Example |
|--------|------|------------|---------|
| `docker stop` | `-t` | Timeout before stop | `docker stop -t 5 myapp` |
| `docker rm` | `-f` | Force remove container | `docker rm -f myapp` |
| `docker rmi` | `-f` | Force remove image | `docker rmi -f nginx` |

---

## 🔍 Exec & Logs

| Command | Flag | Description | Example |
|--------|------|------------|---------|
| `docker exec` | `-it` | Run command inside container | `docker exec -it myapp bash` |
| `docker logs` | `-f` | Follow logs | `docker logs -f myapp` |
| `docker logs` | `--tail` | Show last N lines | `docker logs --tail 50 myapp` |

---

## 🧠 Quick DevOps Tip
Avoid using the `latest` tag in production.  
Always pin **versioned tags** for stability and reproducibility.

---
