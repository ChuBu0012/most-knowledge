---
title: "How-To: ดูข้อมูลเครื่อง (ชื่อ, OS, Kernel, CPU, RAM, Disk)"
aliases:
  - เช็กสเปกเครื่อง
  - ดู os version
  - ubuntu version
  - เครื่องนี้ arm หรือ x86
  - system info
tags: [linux, how-to, system]
type: how-to
status: published
---

# ดูข้อมูลเครื่อง

| อยากรู้ | คำสั่ง |
|---|---|
| ชื่อเครื่อง | `hostname` |
| IP ของเครื่อง | `hostname -I` (macOS: `ipconfig getifaddr en0`) |
| Distro + เวอร์ชัน | `cat /etc/os-release` (macOS: `sw_vers`) |
| Kernel | `uname -r` |
| CPU เป็น x86 หรือ ARM | `uname -m` → `x86_64` / `aarch64` / `arm64` |
| ทุกอย่างในหน้าเดียว | `hostnamectl` |
| จำนวน CPU core | `nproc` (macOS: `sysctl -n hw.ncpu`) |
| RAM | `free -h` |
| Disk เหลือเท่าไร | `df -h` |
| โฟลเดอร์ไหนกินที่ | `du -sh * \| sort -h` |
| เปิดเครื่องมานานแค่ไหน / load | `uptime` |
| ใครล็อกอินอยู่ | `who` |
| เป็น VM / container ไหม | `systemd-detect-virt` |

## สรุปเครื่องในคำสั่งเดียว (Copy ไปใช้ได้)

```bash
echo "Host:   $(hostname)"; \
echo "OS:     $(. /etc/os-release && echo $PRETTY_NAME)"; \
echo "Kernel: $(uname -r) ($(uname -m))"; \
echo "CPU:    $(nproc) cores"; \
free -h | awk '/Mem:/{print "RAM:    "$3" used / "$2}'; \
df -h / | awk 'NR==2{print "Disk /: "$3" used / "$2" ("$5")"}'
```

## ลึกกว่านี้

[[System-Identity-hostname-uname]] — option ทั้งหมดของ `uname`, hostname เก็บที่ไหน
