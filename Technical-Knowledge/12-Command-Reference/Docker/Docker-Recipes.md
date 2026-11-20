---
title: Docker Recipes
type: reference
tags: [technical-knowledge, docker, infrastructure, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile/
  - https://docs.docker.com/reference/cli/docker/
---

# Docker Recipes

## Build and run an image

```sh
docker build -t myapp:dev .
docker run --rm -p 3000:3000 --env-file .env myapp:dev
```

Do not bake secrets into image layers or commit `.env`; pass runtime secrets through secret manager/platform.

## Write a small production Dockerfile

```dockerfile
FROM node:22-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:22-alpine
ENV NODE_ENV=production
WORKDIR /app
COPY --from=build /app/package*.json ./
RUN npm ci --omit=dev
COPY --from=build /app/dist ./dist
USER node
EXPOSE 3000
CMD ["node", "dist/server.js"]
```

Use a `.dockerignore`, pin base image/digest for reproducibility, run as non-root, and copy only runtime artifacts. Adapt package manager and entry point; multi-stage builds avoid shipping compiler/development dependencies.

## Inspect containers and logs

```sh
docker ps -a
docker logs --tail=100 -f <container>
docker exec -it <container> sh
docker inspect <container>
```

Avoid printing secrets from env during incident debugging; prefer health/log output and minimal shell access.

## Persist data

Use named volumes for state that must survive container replacement. Container writable layer is ephemeral. Back up and test restore of database volumes; do not mount production data into arbitrary local containers.

## Clean up

`docker stop`, `docker rm`, `docker image prune` remove resources; inspect targets before destructive prune commands. Never use broad volume prune without confirming no needed data is stored there.

## Read next

[[Docker Image Layers and Reproducible Builds]] · [[Docker Compose Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
