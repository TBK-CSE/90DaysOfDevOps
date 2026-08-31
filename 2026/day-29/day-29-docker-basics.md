# Day 29 – Introduction to Docker

## Task
Understand what Docker is and run the first container.

**Covers:**
- Why containers exist and how they differ from VMs
- Installing Docker
- Running and exploring containers from Docker Hub

---

## Task 1: What is Docker?

**What is a container, and why do we need it?**
A container packages an app with all its dependencies so it runs consistently anywhere. Solves the "works on my machine" problem — lightweight and portable.

**Containers vs Virtual Machines**
Containers share the host OS — lightweight and fast. VMs run a full separate OS each — heavier and slower, but with stronger isolation.

**Docker Architecture**
Docker consists of a client (CLI), daemon (engine), images (templates), containers (running apps), and a registry (stores images).

**Flow:** client → daemon → image → container

*[screenshot: Docker architecture diagram]*

**Breakdown:**
- **Client** → sends commands
- **Docker Daemon** → runs containers
- **Images** → blueprints
- **Containers** → running app instances
- **Registry (Docker Hub)** → where images come from

---

## Task 2: Install Docker

1. Install Docker (locally or on a cloud instance)
2. Verify the installation
3. Run the `hello-world` container
4. Read the output carefully — it explains what just happened

*[screenshot: docker run hello-world]*

Ran the `hello-world` image from Docker Hub. Since it wasn't present locally, the Docker Daemon (`dockerd`) pulled it from the registry first, then ran the container.

---

## Task 3: Run Real Containers

1. Run an **Nginx** container, access it via browser
2. Run an **Ubuntu** container in interactive mode — explore it like a mini Linux machine
3. List running containers
4. List all containers (including stopped)
5. Stop and remove a container

*[screenshot: Nginx container running]*
*[screenshot: Ubuntu container interactive + container listing]*

---

## Task 4: Explore

1. Run a container in **detached mode** — what's different?
2. Give a container a custom **name**
3. Map a **port** from container to host
4. Check **logs** of a running container
5. Run a command **inside** a running container

*[screenshot: detached mode, named container, port mapping]*
*[screenshot: container logs and exec-into-container]*
