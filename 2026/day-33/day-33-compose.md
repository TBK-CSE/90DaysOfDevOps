# Day 33 – Docker Compose: Multi-Container Basics

## Task
Run multi-container applications with a single command.

Yesterday, networks and volumes were created manually and containers run one by one. Docker Compose does all of that from a single YAML file.

---

## Task 1: Install & Verify

Checked Docker Compose availability and version:
```
docker compose version
```
**Output:** Docker Compose version v5.1.3

---

## Task 2: First Compose File

1. Create folder `compose-basics`
2. Write a `docker-compose.yml` running a single Nginx container with port mapping
3. Start with `docker compose up`
4. Access via browser
5. Stop with `docker compose down`

**`docker-compose.yml`:**
```yaml
services:
  nginx:
    image: nginx
    ports:
      - "8080:80"
```

*[screenshot: docker compose up output]*
*[screenshot: Nginx page in browser]*
*[screenshot: docker compose down output]*

---

## Task 3: Two-Container Setup (WordPress + MySQL)

Compose file running:
- A **WordPress** container
- A **MySQL** container

Both on the same auto-created network, MySQL with a named volume for persistence, WordPress connecting to MySQL via service name.

**`docker-compose.yml`:**
```yaml
version: "3.8"
services:
  db:
    image: mysql:5.7
    container_name: mysql-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppass
    volumes:
      - db_data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    container_name: wordpress-app
    restart: always
    ports:
      - "8081:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppass
      WORDPRESS_DB_NAME: wordpress
    depends_on:
      - db

volumes:
  db_data:
```

*[screenshot: WordPress application UI]*

**Verified persistence:** stopped and restarted with `docker compose down` + `docker compose up` — WordPress data was still there.

*[screenshot: data persisted after restart]*

---

## Task 4: Compose Commands

| Action | Command |
|---|---|
| Start in detached mode | `docker compose up -d` |
| View running services | `docker compose ps` |
| View logs (all services) | `docker compose logs -f` |
| View logs (specific service) | `docker compose logs -f wordpress` |
| Stop without removing | `docker compose stop` |
| Remove everything (containers, networks) | `docker compose down` |
| Rebuild after a change | `docker compose up -d --build` |

---

## Task 5: Environment Variables

1. Added environment variables directly in `docker-compose.yml`
2. Created a `.env` file, referenced its variables from the compose file
3. Verified the variables were picked up correctly

*[screenshot: .env file contents]*
*[screenshot: compose file referencing .env variables]*
