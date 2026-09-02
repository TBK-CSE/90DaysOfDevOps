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

*[screenshot: pulled images and sizes]*

**Observation:** `nginx` had the largest disk usage and size among the three.

**Why is Alpine so much smaller?**
- Alpine → minimal Linux, stripped down to essentials
- Ubuntu → full OS with much more baked in

**`docker inspect nginx`** — showed layers, config, environment, ports, OS, architecture, and metadata.

*[screenshot: docker inspect output]*

---

## Task 2: Image Layers

1. `docker image history nginx` — see what layers exist
2. Each line is a **layer**; some show sizes, some show `0B`
3. What are layers, and why does Docker use them?

*[screenshot: docker image history output]*

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

*[screenshot: full lifecycle walkthrough]*

---

## Task 4: Working with Running Containers

1. Run an Nginx container in detached mode
2. View logs
3. View real-time logs (follow mode)
4. Exec into the container, explore the filesystem
5. Run a single command inside without entering the container
6. Inspect the container — IP address, port mappings, mounts

*[screenshot: logs, exec, and inspect output]*

---

## Task 5: Cleanup

1. Stop all running containers in one command
2. Remove all stopped containers in one command
3. Remove unused images
4. Check Docker's total disk usage

*[screenshot: stop all containers]*
*[screenshot: remove stopped containers]*
*[screenshot: remove unused images]*
*[screenshot: docker disk usage]*

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
