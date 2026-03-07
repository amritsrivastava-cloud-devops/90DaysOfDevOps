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
docker run -d \
--name mysql-test \
-e MYSQL_ROOT_PASSWORD=root \
mysql
```

