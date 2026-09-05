# Day 35 – Multi-Stage Builds & Docker Hub

## Task
Build optimized images and share them with the world. Multi-stage builds are how real teams ship small, secure images. Docker Hub is how you distribute them. Both common interview topics.

---

## Task 1: The Problem with Large Images

1. Write a simple Node.js "Hello World" app
2. Build it in a **single stage**
3. Check the image size

**Result:** initial single-stage image size — **1.5GB**

*[screenshot: single-stage image size]*

**`Dockerfile`:**
```dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "app.js"]
```

**`app.js`:**
```javascript
console.log("Hello from Vishal 🚀");
```

---

## Task 2: Multi-Stage Build

1. Rewrote the Dockerfile using multi-stage build:
   - **Stage 1** — build the app (install dependencies, compile)
   - **Stage 2** — copy only the built artifact into a minimal base image (`alpine`)
2. Rebuilt and compared sizes

*[screenshot: multi-stage image size]*

**Result:** size dropped from **1.5GB → 181MB**.

**Why multi-stage is so much smaller:**
Multi-stage removes:
- Build tools
- Build cache
- Unnecessary intermediate dependencies

Only the final compiled app gets copied into the last stage — earlier stages exist purely as intermediate build layers and never ship in the final image.

---

## Task 3: Push to Docker Hub

1. Created a Docker Hub account
2. Logged in from the terminal
3. Tagged the image: `yourusername/image-name:tag`
4. Pushed to Docker Hub
5. Pulled it back (after removing locally) to verify

*[screenshot: docker login]*
*[screenshot: docker tag + push]*
*[screenshot: docker pull verification]*

---

## Task 4: Docker Hub Repository

1. Checked the pushed image on Docker Hub
2. Added a description to the repository
3. Explored the tags tab to understand versioning
4. Compared pulling a specific tag vs `latest`

**Tags used:**
- `warriorr/my-app:v1` — specific version
- `warriorr/my-app:latest` — default tag

---

## Task 5: Image Best Practices

Applied to one image and rebuilt:
1. Minimal base image (Alpine vs Ubuntu — compared sizes)
2. **Non-root user** — added `USER` in the Dockerfile
3. Combined `RUN` commands to reduce layer count
4. **Specific version tags** for base images (not `latest`)

**Optimized `Dockerfile`:**
```dockerfile
# Use minimal base image (specific version, not latest)
FROM node:18.17-alpine

WORKDIR /app

# Create non-root user
RUN adduser -D appuser

# Copy only package files first (better caching)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy remaining app files
COPY . .

# Change ownership to non-root user
RUN chown -R appuser /app

# Switch to non-root user
USER appuser

EXPOSE 3000

CMD ["node", "app.js"]
```

*[screenshot: image size after applying best practices]*

**Result:** image size came down to **237MB** — not multi-stage this time, but with the added security of a non-root user and a minimal base.
