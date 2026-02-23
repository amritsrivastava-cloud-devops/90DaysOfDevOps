# Day 31 – Dockerfile: Build Your Own Images

## Challenge Tasks

### Task 1: Your First Dockerfile
1. Create a folder called `my-first-image`
2. Inside it, create a `Dockerfile` that:
   - Uses `ubuntu` as the base image
   - Installs `curl`
   - Sets a default command to print `"Hello from my custom image!"
3. Build the image and tag it `my-ubuntu:v1`
4. Run a container from your image

```
vi Dockerfile
```

```
FROM ubuntu:22.04

RUN apt-get update && apt-get install -y curl

CMD ["echo", "Hello from my custom image!"]
```

```
docker build -t name:tag .
docker run image-name
```

<img width="822" height="395" alt="image" src="https://github.com/user-attachments/assets/459fed3a-a1c9-4d16-bd18-6870fd5ea7ed" />



**Verify:** The message prints on `docker run`

---

### Task 2: Dockerfile Instructions
Create a new Dockerfile that uses **all** of these instructions:
- `FROM` — base image
- `RUN` — execute commands during build
- `COPY` — copy files from host to image
- `WORKDIR` — set working directory
- `EXPOSE` — document the port
- `CMD` — default command

Build and run it. Understand what each line does.

<img width="1044" height="835" alt="image" src="https://github.com/user-attachments/assets/3e41762a-9170-43a6-bcec-d61d0c0476b3" />



---

### Task 3: CMD vs ENTRYPOINT
1. Create an image with `CMD ["echo", "hello"]` — run it, then run it with a custom command. What happens?
2. Create an image with `ENTRYPOINT ["echo"]` — run it, then run it with additional arguments. What happens?
3. Write in your notes: When would you use CMD vs ENTRYPOINT?

<img width="894" height="617" alt="image" src="https://github.com/user-attachments/assets/523a17c6-2860-4568-a176-bbc7b27af09a" />
<img width="1161" height="386" alt="image" src="https://github.com/user-attachments/assets/cb106983-7ed3-42de-ad7a-a94f1c569a65" />

```
CMD vs ENTRYPOINT (Conclusion)
CMD → Default command, can be replaced
ENTRYPOINT → Fixed command, arguments are appended

Best practice:
CMD for flexibility
ENTRYPOINT for executables
```
---

### Task 4: Build a Simple Web App Image
1. Create a small static HTML file (`index.html`) with any content
2. Write a Dockerfile that:
   - Uses `nginx:alpine` as base
   - Copies your `index.html` to the Nginx web directory
3. Build and tag it `my-website:v1`
4. Run it with port mapping and access it in your browser

<img width="1162" height="516" alt="image" src="https://github.com/user-attachments/assets/5e6569cc-fd0c-4109-aa50-03ed1247d7fa" />
<img width="1765" height="990" alt="image" src="https://github.com/user-attachments/assets/4d636639-1f30-4def-b1c8-3e7ed647ad65" />

---

### Task 5: .dockerignore
1. Create a `.dockerignore` file in one of your project folders
2. Add entries for: `node_modules`, `.git`, `*.md`, `.env`
3. Build the image — verify that ignored files are not included

<img width="1149" height="442" alt="image" src="https://github.com/user-attachments/assets/ee72d782-c7b2-46e5-abb2-25259d6e54e5" />
<img width="942" height="499" alt="image" src="https://github.com/user-attachments/assets/bab3dc4c-b7cf-466a-8455-47d3acb427f2" />

---

### Task 6: Build Optimization
1. Build an image, then change one line and rebuild — notice how Docker uses **cache**
2. Reorder your Dockerfile so that frequently changing lines come **last**
3. Write in your notes: Why does layer order matter for build speed?

---
