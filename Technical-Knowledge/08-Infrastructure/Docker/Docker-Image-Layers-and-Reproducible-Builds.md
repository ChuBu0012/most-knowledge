---
title: "Docker Image Layers and Reproducible Builds"
type: concept
domain: docker
level: intermediate-to-advanced
tags: [docker, containers, supply-chain]
status: researched
last_verified: 2026-11-20
sources:
  - https://docs.docker.com/build/building/best-practices/
---

# Docker Image Layers and Reproducible Builds

## Overview

image เป็น filesystem layers แบบ immutable พร้อม metadata; container เพิ่ม writable layer ตอนรัน

## กลไกและแนวคิดหลัก

คำสั่ง Dockerfile แต่ละขั้นสร้าง layer ที่ cache ได้ตาม input. Multi-stage build แยก build toolchain ออกจาก runtime image. `COPY` order มีผลต่อ cache invalidation; `.dockerignore` ลด context และป้องกันไฟล์ลับถูกส่งไป daemon. Image digest ระบุ content แบบ immutable

## ตัวอย่าง

```typescript
FROM golang:1.27.4 AS build
WORKDIR /src
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 go build -o /out/api ./cmd/api

FROM gcr.io/distroless/static-debian12
COPY --from=build /out/api /api
USER nonroot:nonroot
ENTRYPOINT ["/api"]
```

ตัวอย่างเป็น schematic ที่สื่อหลักการ; ตรวจ syntax และ config ให้ตรงกับ version/runtime ที่ใช้งานก่อนนำไป deploy

## จุดพลาดและข้อควรระวัง

อย่าใส่ secret ด้วย `ARG`/`ENV` ใน layer; ใช้ build secrets; tag `latest` ไม่ reproducible; อย่าใส่ compiler/source/cache ใน production image โดยไม่จำเป็น; root process เพิ่ม blast radius

## แนวทางปฏิบัติ

pin base image/digest ตาม policy, สแกน SBOM/vulnerabilities, build ด้วย least privilege และ rebuild เมื่อ base/security updates เปลี่ยน

## ความสัมพันธ์

[[Docker]] · [[Docker-Compose]] · [[Nginx]] · [[Go]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://docs.docker.com/build/building/best-practices/)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
