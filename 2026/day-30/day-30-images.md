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
