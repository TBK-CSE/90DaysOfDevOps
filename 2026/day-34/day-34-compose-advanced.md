# Day 34 – Docker Compose: Real-World Multi-Container Apps

## Task
Build more complex, production-like setups with Docker Compose. Yesterday was basics — today: app + database + cache, healthchecks, restart policies, and service dependencies.

---

## Task 1: Build a 3-Service App Stack

- **Web app** — Python Flask
- **Database** — Postgres
- **Cache** — Redis

*[screenshot: application running]*

**`docker-compose.yml`:**
```yaml
version: "3.8"

services:
    db:
      image: postgres
      restart: always
      environment:
          POSTGRES_USER: user
          POSTGRES_PASSWORD: pass
          POSTGRES_DB: mydb
      volumes:
        - db_data:/var/lib/postgresql
      networks:
        - app-net
      healthcheck:
        test: ["CMD-SHELL", "pg_isready -U user"]
        interval: 5s
        timeout: 5s
        retries: 5

    redis:
        image: redis
        networks:
          - app-net

    web:
      build: ../app
      ports:
        - "5000:5000"
      depends_on:
        db:
          condition: service_healthy
      networks:
        - app-net

volumes:
  db_data:

networks:
  app-net:
```

**`Dockerfile`:**
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

**`app.py`:**
```python
from flask import Flask
import psycopg2
import redis
import time

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello from Vishal 🚀"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

## Task 2: `depends_on` & Healthchecks

1. Added `depends_on` so the app starts after the database
2. Added a healthcheck on the database service
3. Used `depends_on` with `condition: service_healthy` — app waits for the DB to be truly ready, not just "started"

**Result:** confirmed — the web service now waits until the database passes its healthcheck before starting (see Task 1's compose file for the exact config).

---

## Task 3: Restart Policies

Added `restart: always` to the database service.

**Test:**
```
docker ps
docker kill <db-container-id>
```

**Observation:** the container did *not* auto-restart from a manual kill — restart policies only kick in when the container exits due to an actual error/crash.

**Difference between policies:**
- **`always`** → restarts regardless of exit status, even after a clean/manual stop
- **`on-failure`** → restarts only when the container exits with a non-zero code (an actual crash/error)

---

## Task 4: Custom Dockerfiles in Compose

Used `build:` instead of a pre-built image:
```yaml
build: ./app
```
Made a code change, rebuilt and restarted with a single command (`docker compose up -d --build`).

---

## Task 5: Named Networks & Volumes

Already in place from Task 1:
```yaml
networks:
  app-net:

volumes:
  db_data:
```

**Result:**
- DB data persists across restarts
- Containers communicate with each other by service name

---

## Task 6: Scaling (Bonus)

```
docker compose up --scale web=3
```

**Problem:** port conflict — `5000` already bound.

**Why scaling fails with static port mapping:** multiple container replicas can't all bind to the same host port simultaneously — a fixed `host:container` port mapping only works for a single instance.

---

## What I Learned
- Multi-container apps using Docker Compose
- `depends_on` + healthcheck ensures proper startup order
- Restart policies manage container failure recovery
- Custom Dockerfiles can be built directly via Compose
- Networks enable service-to-service communication by name
- Volumes persist database data across restarts

## Observations
- App correctly waits for DB readiness thanks to the healthcheck
- DB does *not* auto-restart on a manual kill (only on actual failure, depending on policy)
- Scaling breaks due to static port conflicts
