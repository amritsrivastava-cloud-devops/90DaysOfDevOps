# Day 32 – Docker Volumes & Networking

## Objective
Understand how Docker handles **data persistence** and **container communication** using volumes and networks.

Containers are ephemeral. If a container is removed, its internal data is lost unless it is stored outside the container using **volumes or bind mounts**.

---

# Task 1 – The Problem (Data Loss)

## Step 1: Run a MySQL Container

```bash
docker run -d --name mysql-test -e MYSQL_ROOT_PASSWORD=root mysql
```

## Step 2: Enter the container

```bash
docker exec -it mysql-test bash

mysql -uroot -p
```

```bash

CREATE DATABASE testdb;
USE testdb;

CREATE TABLE users (
id INT PRIMARY KEY,
name VARCHAR(50)
);

INSERT INTO users VALUES (1,'Amrit');
SELECT * FROM users;
```

## Step 3: Remove container

```
docker stop mysql-test
docker rm mysql-test
```
## Step 4: Recreate container 
```
docker run -d --name mysql-test -e MYSQL_ROOT_PASSWORD=root mysql
```

#### Because container storage is ephemeral. When the container is deleted, its writable layer is also deleted.

# Task 2 – Named Volumes

## Step 1: Create Volume
```bash
# Create volume 
docker volume create mysql-data

docker volume ls

# Run MySQL with volume
docker run -d --name mysql-vol -e MYSQL_ROOT_PASSWORD=root -v mysql-data:/var/lib/mysql mysql
docker stop mysql-vol

# Remove container
docker rm mysql-vol

# Run new container with same volume
docker run -d --name mysql-vol2 -e MYSQL_ROOT_PASSWORD=root -v mysql-data:/var/lib/mysql mysql

# Verify volume details
docker volume inspect mysql-data
```

# Task 3 – Bind Mounts

## Step 1: Create folder on host
```
mkdir mywebsite
cd mywebsite
vi index.html
<h1>Hello from Docker Bind Mount</h1>
```

## Step 2: Run Nginx container
```
docker run -d --name nginx-test -p 8080:80 -v $(pwd):/usr/share/nginx/html nginx
http://localhost:8080
```
## Step 3: Edit HTML file on host
```
vi index.html

Change text.
Refresh browser.
Result - Changes appear instantly.
```

| Feature           | Named Volume               | Bind Mount                     |
| ----------------- | -------------------------- | ------------------------------ |
| Managed by Docker | Yes                        | No                             |
| Location          | `/var/lib/docker/volumes`  | Any host directory             |
| Use case          | Databases, persistent data | Development, live file editing |
| Portability       | High                       | Depends on host path           |

# Task 4 – Docker Networking Basics
```
docker network ls
docker network inspect bridge
docker run -dit --name container1 ubuntu bash
docker run -dit --name container2 ubuntu bash
apt update
apt install iputils-ping -y
ping container2

Result

❌ Name ping does not work.

Try ping by IP.
First get IP:
docker inspect container2
Ping using IP.
Result

✔ IP ping works.
```

# Task 5 – Custom Network
```
## Create custom network:
docker network create my-app-net
## Run containers on it:
docker run -dit --name app1 --network my-app-net ubuntu bash
docker run -dit --name app2 --network my-app-net ubuntu bash
## Ping by name
docker exec -it app1 ping app2
```
### Result

✔ Name ping works.

### Why?

- Custom networks provide built-in DNS resolution, allowing containers to communicate using container names.
- Default bridge network does not provide automatic name resolution.

# Task 6 – Put It Together
```
## Create network:
docker network create app-network
## Create volume:
docker volume create postgres-data
## Run Postgres container:
docker run -d --name postgres-db --network app-network -e POSTGRES_PASSWORD=root -v postgres-data:/var/lib/postgresql/data postgres
## Run application container:
docker run -dit --name app-container --network app-network ubuntu bash
## Test connectivity
docker exec -it app-container ping postgres-db
```

### Result
The application container can reach the database container using the container name


## Key Learnings
- Containers are ephemeral, so data disappears when containers are removed.
- Named volumes persist data outside containers.
- Bind mounts link host directories to containers.
- Default Docker bridge allows communication by IP only.
- Custom networks enable DNS-based container communication.
- Combining volumes + custom networks is essential for real applications.

## Screenshots
- MySQL container without volume
- Volume creation
- Data persistence test
- Bind mount with Nginx
- Docker networks list
- Custom network ping test

## Conclusion
- Docker volumes solve the data persistence problem, while Docker networks solve the container communication problem.
- These two concepts are fundamental when running real applications like web app + database architectures.
