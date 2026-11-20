---
title: Docker Compose Recipes
type: reference
tags: [technical-knowledge, docker-compose, infrastructure, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://docs.docker.com/compose/gettingstarted/
  - https://docs.docker.com/reference/cli/docker/compose/
---

# Docker Compose Recipes

## Start a local stack

```sh
docker compose up -d --build
docker compose ps
docker compose logs -f api
docker compose down
```

`down` removes containers/network but keeps named volumes unless `-v` is added. `down -v` is destructive to persisted local data.

## Define API + database + health dependency

```yaml
services:
  api:
    build: .
    ports: ["3000:3000"]
    environment:
      DATABASE_URL: postgres://app:devpass@db:5432/app
    depends_on:
      db:
        condition: service_healthy
  db:
    image: postgres:17
    environment:
      POSTGRES_USER: app
      POSTGRES_PASSWORD: devpass
      POSTGRES_DB: app
    volumes: ["dbdata:/var/lib/postgresql/data"]
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U app -d app"]
      interval: 5s
      timeout: 3s
      retries: 10
volumes:
  dbdata:
```

`depends_on` controls startup ordering; health check is needed to wait for readiness. For team/prod, use secrets and non-default credentials; do not commit real passwords.

## Run one-off command / inspect service

```sh
docker compose exec api sh
docker compose run --rm api npm run migrate
docker compose config
```

`exec` runs inside existing service; `run` creates a one-off container. Review rendered config for interpolated secrets before sharing output.

## Profiles and environment overrides

Use profiles for optional local tools; use override files for dev-only ports/bind mounts. Keep production secrets outside compose YAML and avoid mounting source in production.

## Read next

[[Docker Compose Service Networking and Health]] · [[Docker Recipes]] · [[Nginx Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
