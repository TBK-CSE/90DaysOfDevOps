# Day 32 – Docker Volumes & Networking

## Task
Solve two real problems: data persistence and container communication.

Containers are ephemeral — they lose data when removed. And by default, containers can't easily talk to each other. Fixing both today.

---

## Task 1: The Problem

1. Run a Postgres or MySQL container
2. Create some data inside it (table, rows — anything)
3. Stop and remove the container
4. Run a new one — is the data still there?

*[screenshot: table created with data]*

Created a table and inserted data successfully.

*[screenshot: data gone after container re-creation]*

After re-creating the same image, all data was lost — the data was never persisted anywhere outside the container itself.

**Why:** Containers are ephemeral — anything stored inside a container's own filesystem is lost the moment the container is removed.

---

## Task 2: Named Volumes

1. Create a named volume
2. Run the same database container, this time with the volume attached
3. Add data, stop and remove the container
4. Run a new container with the same volume
5. Is the data still there?

**Verify with:** `docker volume ls`, `docker volume inspect`

*[screenshot: volume creation and attachment]*

Data was still there — even after fully re-creating the container — because it was written to the mounted volume, not the container's own filesystem.

*[screenshot: data persisted after container re-creation]*
*[screenshot: docker volume inspect output]*

**Key insight:**
- The **container** thinks it's storing data at `/var/lib/postgresql`
- **Docker** actually stores that data on the host at `/var/lib/docker/volumes/my-db-data/_data`

That host-side location is where the data truly lives — not inside the container.

---

## Task 3: Bind Mounts

1. Create a folder on the host with an `index.html`
2. Run an Nginx container, **bind mount** that folder to the Nginx web directory
3. Access the page in browser
4. Edit `index.html` on the host, refresh browser

*[screenshot: bind mount setup]*
*[screenshot: page output in browser]*

Edited `index.html` (added "part 2" at the end), saved — change reflected immediately on refresh.

*[screenshot: live-edited page]*

**Named volume vs bind mount:**
- **Named volume** → managed entirely by Docker
- **Bind mount** → direct link to a specific host folder

**When to use which:**
- **Bind mount** → local dev work, live editing
- **Named volume** → databases, persistent production storage

---

## Task 4: Docker Networking Basics

1. List all Docker networks
2. Inspect the default `bridge` network
3. Run two containers on the default bridge — can they ping each other by **name**?
4. Can they ping each other by **IP**?

*[screenshot: docker network ls]*
*[screenshot: docker network inspect bridge]*

```bash
docker run -dit --name c1 ubuntu
docker run -dit --name c2 ubuntu
```

*[screenshot: ping attempt — ping not installed]*

`ping` wasn't installed initially — installed it inside the containers first.

*[screenshot: ping working by IP, failing by name]*

**Result:** pinging by IP worked; pinging by container name did not, on the default bridge network.

---

## Task 5: Custom Networks

1. Create a custom bridge network `my-app-net`
2. Run two containers on it
3. Can they ping each other by name now?

*[screenshot: successful name-based ping on custom network]*
*[screenshot: commands used]*

**Result:** name-based ping worked once containers were placed on the custom network.

**Default bridge vs custom network:**
- **Default bridge** → IP-based ping works, name-based doesn't
- **Custom network** → both work

**Why:** custom Docker networks provide built-in DNS resolution between containers; the default bridge network does not.

---

## Task 6: Put It Together

1. Create a custom network
2. Run a database container (MySQL/Postgres) on it, with a volume for data
3. Run an app container on the same network
4. Verify the app container can reach the database by name

*[screenshot: successful ping from app container to db container by name]*
*[screenshot: commands used]*

Successfully pinged from an Ubuntu container to a Postgres container named `db`, purely by container name.

**Note:** the default bridge network could technically work too, but only by IP — using a custom network is what enables name-based service discovery.
