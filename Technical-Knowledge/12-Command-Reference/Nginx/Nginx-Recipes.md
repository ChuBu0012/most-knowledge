---
title: Nginx Recipes
type: reference
tags: [technical-knowledge, nginx, infrastructure, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://nginx.org/en/docs/beginners_guide.html
  - https://nginx.org/en/docs/http/ngx_http_proxy_module.html
---

# Nginx Recipes

## Reverse proxy to application

```nginx
server {
    listen 80;
    server_name example.com;
    location / {
        proxy_pass http://app:3000;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Only trust forwarded headers from known proxy hops. Configure app proxy trust to match topology so clients cannot spoof IP/scheme.

## Validate and reload

```sh
nginx -t
nginx -s reload
```

Validate config before reload; use service manager/container orchestration in production. Keep previous known-good config for rollback.

## Set client body and timeouts

Use `client_max_body_size`, `proxy_connect_timeout`, `proxy_read_timeout`, and `proxy_send_timeout` based on application behavior. Set limits deliberately to reduce resource exhaustion; larger timeout is not always safer.

## TLS termination

Listen on 443 with certificate/key paths from protected secret/certificate provisioning; configure modern TLS policy from maintained deployment guidance and automate renewal. Redirect HTTP to HTTPS only after certificate routing is correct.

## Static files and cache

Use `root`/`try_files` for static assets; set immutable caching only for content-hashed filenames. Ensure SPA fallback is used only for client-routed apps; APIs should return real 404s.

## Observe

Tail access/error logs, check upstream status and latency; do not log authorization headers, cookies, or sensitive query params.

## Read next

[[Nginx Reverse Proxy Request Flow]] · [[Docker Compose Recipes]] · [[HTTP Request Lifecycle]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
