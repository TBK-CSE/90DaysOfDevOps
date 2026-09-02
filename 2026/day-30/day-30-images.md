# Day 30 – Docker Images & Container Lifecycle

## Task
Understand how images and containers actually work.

**Covers:**
- Relationship between images and containers
- Image layers and caching
- The full container lifecycle

---

## Task 1: Docker Images

1. Pull `nginx`, `ubuntu`, and `alpine` from Docker Hub
2. List all local images — note sizes
3. Compare `ubuntu` vs `alpine` — why is one much smaller?
4. Inspect an image
5. Remove an unneeded image

<img width="921" height="685" alt="image" src="https://github.com/user-attachments/assets/d69bd72d-d1d2-40e3-8e35-6df6286364fe" />


**Observation:** `nginx` had the largest disk usage and size among the three.

**Why is Alpine so much smaller?**
- Alpine → minimal Linux, stripped down to essentials
- Ubuntu → full OS with much more baked in

**`docker inspect nginx`** — showed layers, config, environment, ports, OS, architecture, and metadata.

<img width="1034" height="967" alt="image" src="https://github.com/user-attachments/assets/ef954c67-c93f-4778-b43f-147ff0f0ff4a" />
---

## Task 2: Image Layers

1. `docker image history nginx` — see what layers exist
2. Each line is a **layer**; some show sizes, some show `0B`
3. What are layers, and why does Docker use them?

<img width="1074" height="414" alt="image" src="https://github.com/user-attachments/assets/ba0a4758-1b54-411f-b22e-69c216ceb034" />


**Layers:**
- Represent incremental changes on top of a base image
- Reused across builds → faster build times
- Save storage since unchanged layers aren't rebuilt

**How layers get created:**
```
Base image → ubuntu
apt update → new layer
install nginx → new layer
copy files → new layer
```
Each step = one incremental layer.

**Layer reuse example:** if only the `COPY` step changes, Docker reuses all previous layers and only rebuilds from that point — much faster than a full rebuild.

---

## Task 3: Container Lifecycle

Full lifecycle practiced on one container:
1. **Create** (without starting)
2. **Start**
3. **Pause** — check status
4. **Unpause**
5. **Stop**
6. **Restart**
7. **Kill**
8. **Remove**

`docker ps -a` checked after each step to observe state changes.
<img width="1018" height="850" alt="image" src="https://github.com/user-attachments/assets/5cf86e1b-a8c9-41b1-bfe7-d1befaaffeb3" />



---

## Task 4: Working with Running Containers

1. Run an Nginx container in detached mode
2. View logs
3. View real-time logs (follow mode)
4. Exec into the container, explore the filesystem
5. Run a single command inside without entering the container
6. Inspect the container — IP address, port mappings, mounts

<img width="747" height="191" alt="image" src="https://github.com/user-attachments/assets/64374b63-8793-4bdc-aaff-15a3ca093d6a" />
<img width="931" height="361" alt="image" src="https://github.com/user-attachments/assets/8b931f66-b36a-4fcc-b7ad-5177b815939e" />
<img width="638" height="474" alt="image" src="https://github.com/user-attachments/assets/71e067f1-6d0a-445b-81f4-481d042f09d6" />
<img width="886" height="154" alt="image" src="https://github.com/user-attachments/assets/91209efb-f209-4fb5-ae90-83f603d05515" />



---

## Task 5: Cleanup

1. Stop all running containers in one command
2. Remove all stopped containers in one command
3. Remove unused images
4. Check Docker's total disk usage
<img width="1022" height="173" alt="image" src="https://github.com/user-attachments/assets/ed7a14ee-fa45-47f4-b023-93d4fb6dbbc0" />
<img width="747" height="113" alt="image" src="https://github.com/user-attachments/assets/fc6e94b2-866f-4924-b43f-31ddbd0a7583" />
<img width="945" height="529" alt="image" src="https://github.com/user-attachments/assets/c7c62154-2749-4a12-ae16-c6b8badaa943" />
<img width="640" height="175" alt="image" src="https://github.com/user-attachments/assets/f2b55718-2c64-432f-9f96-e22b5918dc50" />


---

## Container Lifecycle

```
create → start → pause → unpause → stop → restart → kill → remove
```

## Commands Used
`docker pull`, `docker images`, `docker inspect`, `docker image history`, `docker create`, `docker start`, `docker stop`, `docker pause`, `docker unpause`, `docker restart`, `docker kill`, `docker rm`, `docker logs`, `docker exec`, `docker system prune`

## Observations
- Alpine image is very small compared to Ubuntu
- Containers move through distinct states over their lifecycle
- Layers enable faster builds and storage reuse

## What I Learned
- Images are templates for containers
- Containers go through defined lifecycle states
- Docker uses layers to optimize storage and build speed
