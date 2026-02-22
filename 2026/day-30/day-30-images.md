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

**| Image |	Reason |**
| Ubuntu |	Full GNU/Linux utilities, larger base |
| Alpine | Uses musl libc & busybox, minimal OS |

👉 Alpine is preferred for lightweight containers
