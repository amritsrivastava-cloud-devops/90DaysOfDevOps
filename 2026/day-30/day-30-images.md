# Day 30 – Docker Images & Container Lifecycle 🐳

## Objective
Understand how **Docker images** and **containers** work internally, including:
- Image vs container relationship
- Image layers & caching
- Full container lifecycle
- Working with running containers
- Cleanup & disk usage

---

## Task 1: Docker Images

### 1. Pull Images from Docker Hub
```bash
docker pull nginx
docker pull ubuntu
docker pull alpine
```

### 2. List All Images & Sizes
```
ubuntu@ip-172-31-3-172:~$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    bbdabce66f1b   11 days ago   78.1MB
nginx        latest    5cdef4ac3335   2 weeks ago   161MB
alpine       latest    a40c03cbb81c   3 weeks ago   8.44MB
```
### 3. Ubuntu vs Alpine – Why the Size Difference?

| Image |	Reason |
|------|-----|
| Ubuntu |	Full GNU/Linux utilities, larger base |
| Alpine | Uses musl libc & busybox, minimal OS |

👉 Alpine is preferred for lightweight containers

### 4. Inspect an Image

```
docker inspect nginx
```

- Information found:
- Image ID
- Environment variables
- Exposed ports
- Entrypoint & CMD
- Layers & architecture
  
<img width="1543" height="875" alt="image" src="https://github.com/user-attachments/assets/442d284e-d8d1-4622-b15f-fa65192a4897" />

### 5. Remove image 

```
docker rmi imgname
```
<img width="919" height="227" alt="image" src="https://github.com/user-attachments/assets/b5a74525-ff39-4c87-bd79-47fd45f9906f" />

---

## Task 2: Image Layers

### 1. View Image History
```
docker image history nginx
```

<img width="1212" height="367" alt="image" src="https://github.com/user-attachments/assets/26901396-65b0-4c0e-b253-a56f283e86b6" />

### 2. Observations

Each line = one layer
Some layers show 0B (metadata instructions)
Larger layers come from:
Base OS
Installed packages
Application files

### 3. What Are Image Layers?

Image layers are read-only filesystem layers stacked together.

### 4. Why Docker Uses Layers?

Faster builds (layer caching)
Reusability across images
Efficient disk usage
Faster image pulls

---

## Task 3: Container Lifecycle

#### 1. Create (Without Starting)
``` docker create --name nginx-amrit nginx ```
#### 2. Start
``` docker start nginx-amrit ```
#### 3. Pause
``` docker pause nginx-amrit ```
``` docker ps -a ```
#### 4. Unpause
``` docker unpause nginx-amrit ```
#### 5. Stop
``` docker stop nginx-amrit ```
#### 6. Restart
``` docker restart nginx-amrit ```
#### 7. Kill
``` docker kill nginx-amrit ```
#### 8. Remove
``` docker rm nginx-amrit ```

- Checked docker ps -a after each step to observe state changes

<img width="1237" height="755" alt="image" src="https://github.com/user-attachments/assets/40bbde73-aeed-4d90-b499-a30f2ec6e5fe" />
<img width="1378" height="892" alt="image" src="https://github.com/user-attachments/assets/0ff0a581-743b-4479-b42d-8b7e4724349e" />

---

## Task 4: Working with Running Containers

### 1. Run Nginx in Detached Mode
```
docker run -d -p 8080:80 --name nginx-supermario nginx
```

<img width="1711" height="775" alt="image" src="https://github.com/user-attachments/assets/7804fdd9-53fe-4d49-9030-6bf45f2a7287" />

### 2. View Logs
```
docker logs containerid
docker logs containerid -f
```

<img width="1772" height="895" alt="image" src="https://github.com/user-attachments/assets/d845d4c4-755e-4450-9225-a7c25f4bed59" />

### 3. Follow Logs (Real-time)
```
docker exec -it containerid bash
```
<img width="1872" height="937" alt="image" src="https://github.com/user-attachments/assets/91e96f2a-e496-4665-95ac-dd67f1f3044e" />
<img width="1004" height="482" alt="image" src="https://github.com/user-attachments/assets/a708b24a-ca3c-4994-821c-6782f1002fc5" />

### 4. Exec into Container
```
docker exec containerid command
```
<img width="1239" height="501" alt="image" src="https://github.com/user-attachments/assets/e60bde4d-852b-4254-9986-d52ffce6c25f" />

### 5. Inspect Container
```
docker inspect containerid
```

<img width="1395" height="554" alt="image" src="https://github.com/user-attachments/assets/4d519e9b-9cc3-405b-947c-21714df49665" />


