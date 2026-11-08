---
title: Practical Linux Command Cheat Sheet
tags:
  - linux
  - terminal
  - bash
  - cheatsheet
  - reference
  - sysadmin
  - devops
type: reference
status: published
---

# Practical Linux Command Cheat Sheet

> 💡 **ต้องการฉบับย่อ ภาษาไทย อ่านง่าย ใช้งานทันที?** 👉 เปิดอ่านได้ที่ [[Linux-Simple-Guide]]

A workflow-oriented, practical reference manual for everyday Linux terminal operations. Designed to help engineers, developers, and system administrators quickly identify the right command based on **what they want to accomplish**, rather than memorizing syntax in isolation.

---

## How to Use This Cheat Sheet

- **Intent-Driven Navigation:** Sections are categorized by workflow objectives (e.g., searching, inspecting system health, managing processes) rather than alphabetical command names.
- **Visual Safety Indicators:**
  - 🔍 **Inspection:** Safe commands that read or query system state without altering data.
  - ⚙️ **Modification:** Commands that create, modify, or update configurations and files.
  - ⚠️ **High Risk / Destructive:** Commands capable of data destruction, disk formatting, or system instability. Proceed with verification.
- **Elevated Privileges:** Commands requiring `sudo` indicate administrative authorization needed to alter system files, control daemons, or query kernel-level sockets.

---

## Table of Contents

- [Quick Reference Table](#quick-reference-table)
- [1. Navigate and Explore](#1-navigate-and-explore)
  - [`pwd`](#pwd) — Print working directory
  - [`ls`](#ls) — List directory contents
  - [`cd`](#cd) — Change directory
  - [`tree`](#tree) — Visualize directory hierarchy
- [2. Manage Files and Directories](#2-manage-files-and-directories)
  - [`mkdir`](#mkdir) — Create directories
  - [`touch`](#touch) — Create empty files or update timestamps
  - [`cp`](#cp) — Copy files and directories
  - [`mv`](#mv) — Move or rename files and directories
  - [`rm`](#rm) — Remove files and directories
  - [`rmdir`](#rmdir) — Remove empty directories
  - [`find`](#find) — Search files by attributes
  - [`which` / `whereis`](#which-whereis) — Locate executable binaries and paths
  - [Spotlight: `cp` vs `mv`](#spotlight-cp-vs-mv)
  - [Spotlight: `find` vs `grep` vs `which`](#spotlight-find-vs-grep-vs-which)
- [3. Read and Inspect Files](#3-read-and-inspect-files)
  - [`cat`](#cat) — Concatenate and display file content
  - [`tac`](#tac) — Display file content in reverse line order
  - [`less`](#less) — Interactive paginated viewer
  - [`head`](#head) — Output beginning of files
  - [`tail`](#tail) — Output end of files and monitor live streams
  - [`grep`](#grep) — Search text patterns using regular expressions
  - [`diff`](#diff) — Compare files line by line
  - [`wc`](#wc) — Count lines, words, characters, and bytes
- [4. Edit and Process Text](#4-edit-and-process-text)
  - [`nano`](#nano) — Simple modeless text editor
  - [`vim`](#vim) — Modal command-line text editor
  - [`cut`](#cut) — Extract columns or character fields
  - [`sort`](#sort) — Sort lines of text
  - [`uniq`](#uniq) — Filter or report repeated adjacent lines
  - [`tr`](#tr) — Translate or delete characters
  - [`sed`](#sed) — Stream editor for automated text filtering and transformation
  - [`awk`](#awk) — Pattern-directed text processing language
  - [Pipes and Redirection (`|`, `>`, `>>`, `2>`, `&>`)](#pipes-and-redirection)
  - [`tee`](#tee) — Split output to terminal and files simultaneously
  - [`xargs`](#xargs) — Build and execute commands from standard input
  - [Spotlight: `>` vs `>>`](#spotlight-vs)
- [5. Monitor System Resources](#5-monitor-system-resources)
  - [`top` / `htop`](#top-htop) — Interactive real-time process viewers
  - [`free`](#free) — Check RAM and swap memory usage
  - [`uptime`](#uptime) — System running time and load averages
  - [`vmstat`](#vmstat) — Virtual memory statistics and I/O rates
  - [`df`](#df) — Disk filesystem space and inode usage
  - [`du`](#du) — Disk space consumed by files and folders
  - [`uname`](#uname) — Print kernel and architecture details
  - [`lscpu`](#lscpu) — Display CPU hardware specifications
  - [`lsblk`](#lsblk) — List block storage devices
  - [`hostnamectl`](#hostnamectl) — Inspect and configure system hostname
  - [Spotlight: `df` vs `du`](#spotlight-df-vs-du)
- [6. Manage Processes and Services](#6-manage-processes-and-services)
  - [`ps`](#ps) — Snapshot of current running processes
  - [`pgrep` / `pidof`](#pgrep-pidof) — Search processes by name
  - [`kill`](#kill) — Send signals to terminate or control processes
  - [`pkill` / `killall`](#pkill-killall) — Terminate processes by name or pattern
  - [Background Jobs: `&`, `nohup`, `jobs`, `bg`, `fg`](#background-jobs)
  - [`systemctl`](#systemctl) — Manage systemd system services and units
  - [`journalctl`](#journalctl) — Query and inspect systemd logs
  - [Spotlight: `SIGTERM` (15) vs `SIGKILL` (9)](#spotlight-sigterm-15-vs-sigkill-9)
- [7. Networking](#7-networking)
  - [`ip`](#ip) — Inspect and manage IP addresses and routing tables
  - [`ping`](#ping) — Test host reachability via ICMP echo
  - [`traceroute` / `tracepath`](#traceroute-tracepath) — Trace network packet route hops
  - [`ss`](#ss) — Detailed socket statistics and listening ports
  - [`lsof`](#lsof) — List open files and network connections
  - [`curl`](#curl) — Transfer data over HTTP/HTTPS/FTP
  - [`wget`](#wget) — Non-interactive file downloader
  - [`nc`](#nc) — Netcat utility for arbitrary TCP/UDP connections
- [8. Users and Permissions](#8-users-and-permissions)
  - [`whoami` / `id`](#whoami-id) — Display current user and group identities
  - [`who` / `w`](#who-w) — Show logged-in users and current activities
  - [`sudo`](#sudo) — Execute commands with superuser privileges
  - [`su`](#su) — Switch user identity or spawn a login shell
  - [`chmod`](#chmod) — Modify file access permissions
  - [`chown`](#chown) — Modify file and directory ownership
  - [`chgrp`](#chgrp) — Modify group ownership
  - [`umask`](#umask) — Display or configure default file creation mask
  - [`useradd` / `usermod` / `passwd`](#useradd-usermod-passwd) — Manage user accounts
  - [Spotlight: `su` vs `sudo` vs `sudo -i`](#spotlight-su-vs-sudo-vs-sudo--i)
- [9. Package Management](#9-package-management)
  - [Package Manager Cross-Reference Table](#package-manager-cross-reference-table)
  - [`apt` (Debian, Ubuntu)](#apt-debian-ubuntu)
  - [`dnf` / `yum` (Fedora, RHEL, Rocky, Alma)](#dnf-yum-fedora-rhel-rocky-alma)
  - [`pacman` (Arch Linux)](#pacman-arch-linux)
- [10. Archive and Compression](#10-archive-and-compression)
  - [`tar`](#tar) — Tape archive utility (tarball packaging)
  - [`gzip` / `gunzip`](#gzip-gunzip) — Single-file compression and decompression
  - [`zip` / `unzip`](#zip-unzip) — Cross-platform ZIP archive management
- [11. Storage and Disks](#11-storage-and-disks)
  - [`lsblk` / `blkid`](#lsblk-blkid) — Inspect block devices and filesystem UUIDs
  - [`findmnt`](#findmnt) — Display mounted filesystem trees
  - [`mount` / `umount`](#mount-umount) — Attach and detach filesystems
  - [`fdisk`](#fdisk) — Manipulate disk partition tables
  - [`dd`](#dd) — Low-level raw block copy and conversion
- [12. Shell Productivity](#12-shell-productivity)
  - [`history`](#history) — Command history navigation and re-execution
  - [Environment Variables: `env`, `export`, `unset`](#environment-variables)
  - [Command Aliases: `alias`, `unalias`](#command-aliases)
- [13. Common Command Combinations](#13-common-command-combinations)
- [14. Useful Keyboard Shortcuts](#14-useful-keyboard-shortcuts)
- [15. Common Mistakes and Pitfalls](#15-common-mistakes-and-pitfalls)

---

## Quick Reference Table

| Intent | Command | Quick Example | Description |
|---|---|---|---|
| Current Directory | `pwd` | `pwd` | Print present working directory path |
| List Files | `ls` | `ls -lah` | List all files with details and human-readable sizes |
| Change Directory | `cd` | `cd -` | Switch back to previous working directory |
| Create Folder | `mkdir` | `mkdir -p src/utils` | Create folder hierarchy without throwing errors |
| Copy Files | `cp` | `cp -r src/ dist/` | Copy files or directories recursively |
| Move / Rename | `mv` | `mv old.txt new.txt` | Rename or relocate files and directories |
| Remove Files | `rm` | `rm -i file.txt` | Delete files safely with interactive confirmation |
| Search Files | `find` | `find . -name "*.log" -mtime +7` | Locate files by name, type, modification date |
| Search Text | `grep` | `grep -rn "ERROR" /var/log/` | Search text recursively with line numbers |
| View Big Files | `less` | `less app.log` | Open large files without loading entire content into RAM |
| Follow Logs | `tail` | `tail -f /var/log/syslog` | Stream new log entries in real time |
| Free Memory | `free` | `free -h` | Display available RAM and Swap space |
| Disk Usage | `df` | `df -h` | Check available disk capacity per mounted volume |
| Directory Space | `du` | `du -sh * \| sort -h` | Summarize size of folders in current directory |
| Running Processes| `ps` | `ps aux \| grep nginx` | Snapshot active processes filtered by name |
| Stop Process | `kill` | `kill -15 1234` | Request graceful process termination by PID |
| Control Service | `systemctl` | `sudo systemctl restart nginx`| Restart a background system daemon |
| Query Service Logs| `journalctl` | `journalctl -u nginx -f` | Tail logs for a specific systemd unit |
| Check IP Address | `ip` | `ip -br a` | View assigned IP addresses in brief tabular layout |
| Active Ports | `ss` | `ss -tulpn` | List active listening TCP/UDP sockets with PIDs |
| Open Files / Ports| `lsof` | `lsof -i :8080` | Find process bound to port 8080 |
| HTTP Request | `curl` | `curl -Iv https://example.com` | Fetch HTTP headers and verify response status |
| Change Permission| `chmod` | `chmod 644 file.txt` | Set Read/Write for owner, Read for others |
| Change Owner | `chown` | `sudo chown -R app:app /opt/app`| Recursively assign file ownership to user and group |
| Superuser Exec | `sudo` | `sudo -i` | Open root administrative shell |
| Extract Tarball | `tar` | `tar -xzvf archive.tar.gz` | Decompress and extract `.tar.gz` archive |

---

## 1. Navigate and Explore

Commands for inspecting your location in the filesystem hierarchy and exploring directory trees.

### `pwd`
**Purpose:** Print the absolute path of the current working directory.

```bash
pwd [options]
```

| Option | Description |
|---|---|
| `-L` | Print logical path, preserving symlinks (default shell behavior) |
| `-P` | Print physical path, resolving all symbolic links to real targets |

**Examples:**
```bash
# Print current directory path
pwd

# Resolve symlinks to physical disk location
cd /var/mail
pwd -P
# Output: /var/spool/mail
```

---

### `ls`
**Purpose:** List directory contents and file metadata.

```bash
ls [options] [path]
```

| Option | Description |
|---|---|
| `-l` | Long listing format showing permissions, owner, group, size, and timestamp |
| `-a` | List all files, including hidden entries starting with a dot (`.`) |
| `-h` | Display file sizes in human-readable units (`K`, `M`, `G`) |
| `-t` | Sort entries by modification time, newest first |
| `-r` | Reverse sort order (useful combined with `-lt` to show newest at bottom) |
| `-S` | Sort files by size, largest first |
| `-R` | Recursively list subdirectories |

**Examples:**
```bash
# Standard comprehensive inspection: long, all files, human sizes
ls -lah

# Find recently modified files at the bottom of the list
ls -latr

# Sort files by size to identify largest items
ls -lhS
```

---

### `cd`
**Purpose:** Change the current working directory.

```bash
cd [directory]
```

**Special Arguments:**
- `cd` or `cd ~` — Navigate to the current user's home directory.
- `cd -` — Switch back to the previous working directory (toggles between two paths).
- `cd ..` — Move up one directory level into the parent directory.
- `cd ../..` — Move up two directory levels.
- `cd /` — Navigate to the filesystem root directory.

**Examples:**
```bash
# Jump to user home directory
cd ~

# Move back to previous folder after accidental jump
cd /etc/nginx/conf.d
cd /var/www/html
cd -
# Returns to: /etc/nginx/conf.d
```

---

### `tree`
**Purpose:** Display recursive directory structure in an indented tree diagram.

```bash
tree [options] [path]
```

| Option | Description |
|---|---|
| `-L <level>` | Restrict display depth to `<level>` directories deep |
| `-d` | List directories only (omit files) |
| `-a` | Include hidden files and directories |
| `-I <pattern>` | Exclude entries matching the glob pattern (e.g., `"node_modules|.git"`) |
| `-h` | Print human-readable size for each file |

**Examples:**
```bash
# View project layout up to 2 directories deep, ignoring node_modules
tree -L 2 -I "node_modules"

# Display directory hierarchy only
tree -d -L 3 /etc
```

---

## 2. Manage Files and Directories

Commands for creating, copying, renaming, deleting, and discovering files and folders.

### `mkdir`
**Purpose:** Create new directories in the filesystem.

```bash
mkdir [options] <directory...>
```

| Option | Description |
|---|---|
| `-p` | Create parent directories as needed without raising errors if they exist |
| `-m <mode>` | Set octal file permissions at creation time (e.g., `750`) |
| `-v` | Verbose mode: print a message for each directory created |

**Examples:**
```bash
# Create nested directory tree in one command
mkdir -p project/{src,tests,docs,build}

# Create a restricted directory with 700 permissions
mkdir -m 700 ~/.private_keys
```

---

### `touch`
**Purpose:** Create empty files or update access and modification timestamps of existing files.

```bash
touch [options] <file...>
```

| Option | Description |
|---|---|
| `-c` | Do not create file if it does not already exist |
| `-d <string>` | Parse date/time string instead of current clock time |
| `-m` | Update modification time only |

**Examples:**
```bash
# Create an empty configuration file
touch .env.production

# Create multiple placeholder files simultaneously
touch index.js app.js config.js
```

---

### `cp`
**Purpose:** Copy files and directories from source to destination.

```bash
cp [options] <source> <destination>
```

| Option | Description |
|---|---|
| `-r`, `-R` | Copy directories recursively |
| `-p` | Preserve file attributes (timestamps, ownership, permissions) |
| `-a` | Archive mode: equivalent to `-dpR` (preserves all metadata and symlinks) |
| `-i` | Prompt for confirmation before overwriting existing files |
| `-u` | Update mode: copy only when source is newer than destination |
| `-v` | Verbose output detailing each file copied |

**Examples:**
```bash
# Backup a configuration file before editing
cp -p /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak

# Copy a directory recursively preserving permissions and symlinks
cp -a /var/www/site /var/www/site_backup
```

---

### `mv`
**Purpose:** Move or rename files and directories.

```bash
mv [options] <source> <destination>
```

| Option | Description |
|---|---|
| `-i` | Interactive confirmation before overwriting existing target files |
| `-n` | Do not overwrite an existing file (no-clobber) |
| `-u` | Move only when source file is newer than target file |
| `-v` | Verbose mode: print actions taken |

**Examples:**
```bash
# Rename a file in the same directory
mv old_report.txt q4_report.txt

# Relocate files to a different directory safely
mv -i *.log /var/log/archive/
```

---

### `rm`
**Purpose:** Remove (delete) files and directories permanently.

> [!CAUTION]
> **Destructive Command Warning:** Linux filesystems do not have a "Trash Bin" for command-line deletions. Files deleted with `rm` are unlinked immediately and are generally unrecoverable without forensic tools.

```bash
rm [options] <file...>
```

| Option | Description |
|---|---|
| `-r`, `-R` | Remove directories and their contents recursively |
| `-f` | Force removal: ignore nonexistent files and never prompt |
| `-i` | Prompt for confirmation before every file removal |
| `-I` | Prompt once before removing more than three files or recursively |

**Examples:**
```bash
# Remove a single file with confirmation
rm -i unwanted.txt

# Remove an entire build directory
rm -rf ./build/

# Safe removal of multiple log files
rm -I *.tmp
```

**Common Mistake to Avoid:**
```bash
# DANGEROUS: If $TARGET is unset or empty, this evaluates to: rm -rf /*
rm -rf $TARGET/*

# SAFE PRACTICE: Validate variables or use parameter expansion defaults
rm -rf "${TARGET:?}/"*
```

---

### `rmdir`
**Purpose:** Remove empty directories only.

```bash
rmdir [options] <directory...>
```

| Option | Description |
|---|---|
| `-p` | Remove parent directories if they also become empty after removal |

**Examples:**
```bash
# Safely remove empty directory (fails if directory contains files)
rmdir /tmp/empty_dir

# Remove nested chain of empty directories
rmdir -p parent/child/grandchild
```

---

### `find`
**Purpose:** Search for files and directories in a directory hierarchy based on arbitrary criteria.

```bash
find [path] [expression] [action]
```

| Option / Test | Description |
|---|---|
| `-name <pattern>` | Match filename (case-sensitive, quote globs like `"*.conf"`) |
| `-iname <pattern>`| Match filename case-insensitively |
| `-type <f\|d\|l>` | Restrict search to files (`f`), directories (`d`), or symlinks (`l`) |
| `-size <+n\|-n>` | Match size (e.g., `+100M` for >100 megabytes, `-5k` for <5 kilobytes) |
| `-mtime <+n\|-n>` | Modified time in days (`+7` means older than 7 days, `-1` within 24 hours) |
| `-exec <cmd> {} +`| Execute command on matched files in batch (`{}` is placeholder) |
| `-delete` | Delete matched files directly (always test without `-delete` first!) |

**Examples:**
```bash
# Find all .log files modified within the last 24 hours
find /var/log -type f -name "*.log" -mtime -1

# Find files larger than 100MB
find / -type f -size +100M 2>/dev/null

# Find and delete temporary files older than 30 days
find /tmp/cache -type f -name "*.tmp" -mtime +30 -exec rm -f {} +
```

---

### `which` / `whereis`
**Purpose:** Locate binary executables, source files, and manual pages in `$PATH`.

```bash
which <command>
whereis <command>
```

**Examples:**
```bash
# Show which executable runs when you type 'python3'
which python3
# Output: /usr/bin/python3

# Display binary, source, and man page locations
whereis nginx
# Output: nginx: /usr/sbin/nginx /etc/nginx /usr/share/man/man8/nginx.8.gz
```

---

### Spotlight: `cp` vs `mv`

| Dimension | `cp` (Copy) | `mv` (Move / Rename) |
|---|---|---|
| **Under the Hood** | Reads source bytes and allocates **new inodes and data blocks**. | Same filesystem: Updates directory entry pointer only (**same inode**, instant). Cross-filesystem: Copies then deletes source. |
| **Storage Impact** | Consumes additional disk space equal to file size. | Consumes zero additional disk space when on the same filesystem. |
| **Performance** | O(N) proportional to file size. | O(1) instantaneous on the same filesystem, regardless of size (e.g., 50GB file moves in 1ms). |

---

### Spotlight: `find` vs `grep` vs `which`

- Use **`find`** to search the **filesystem tree by metadata** (filename, size, modification date, file type).
- Use **`grep`** to search **inside the text content** of files.
- Use **`which`** to locate where an **executable binary** resides within your current `$PATH`.

```bash
# 1. find the file
find /etc -name "nginx.conf"

# 2. grep inside the file
grep -i "worker_processes" /etc/nginx/nginx.conf

# 3. which binary runs
which nginx
```

---

## 3. Read and Inspect Files

Commands to view, stream, filter, and compare file contents without modifying them.

### `cat`
**Purpose:** Concatenate and print entire file content to standard output.

```bash
cat [options] [file...]
```

| Option | Description |
|---|---|
| `-n` | Number all output lines |
| `-b` | Number non-empty lines only |
| `-s` | Squeeze repeated blank lines into a single blank line |

**Examples:**
```bash
# Display content with line numbers
cat -n /etc/hosts

# Concatenate multiple files into a single destination
cat part1.txt part2.txt > full_document.txt
```

> [!TIP]
> Avoid using `cat` on large files (e.g., `cat 10GB.log`). It floods your terminal and wastes memory. Use `less`, `head`, or `tail` instead.

---

### `tac`
**Purpose:** Print file content in reverse line order (last line first).

```bash
tac [file...]
```

**Examples:**
```bash
# View newest log entries first without paging
tac /var/log/auth.log | head -n 20
```

---

### `less`
**Purpose:** Interactive paginated file viewer allowing forward and backward navigation without loading the whole file into RAM.

```bash
less [options] <file>
```

| Option | Description |
|---|---|
| `-N` | Display line numbers alongside text |
| `-S` | Truncate (chop) long lines instead of wrapping them |
| `-i` | Ignore case in search strings |

**Key Navigation Shortcuts Inside `less`:**
- `Space` or `f`: Page forward (down).
- `b`: Page backward (up).
- `j` / `k`: Scroll down / up one line (Vim style).
- `/pattern`: Search forward for `pattern`.
- `?pattern`: Search backward for `pattern`.
- `n` / `N`: Next / previous search match.
- `g` / `G`: Jump to start / end of file.
- `F`: Emulate `tail -f` (follow live updates; press `Ctrl+C` to return to normal `less`).
- `q`: Exit `less`.

**Examples:**
```bash
# Read system logs with line numbers and un-wrapped lines
less -NS /var/log/syslog
```

---

### `head`
**Purpose:** Output the beginning (first few lines or bytes) of files.

```bash
head [options] [file...]
```

| Option | Description |
|---|---|
| `-n <count>` | Print first `<count>` lines (default: 10) |
| `-c <bytes>` | Print first `<bytes>` bytes |

**Examples:**
```bash
# Inspect the first 5 lines of a CSV dataset
head -n 5 customers.csv
```

---

### `tail`
**Purpose:** Output the ending portion of files and monitor continuous real-time output.

```bash
tail [options] [file...]
```

| Option | Description |
|---|---|
| `-n <count>` | Print last `<count>` lines (default: 10) |
| `-f` | Follow: keep file open and output appended data live |
| `-F` | Follow with retry: tracks by filename even after log rotation |

**Examples:**
```bash
# View last 50 lines of an application log
tail -n 50 /var/log/nginx/error.log

# Stream and follow live log entries as they arrive
tail -f /var/log/syslog

# Robust log follower that survives logrotate file renames
tail -F /var/log/app/production.log
```

---

### `grep`
**Purpose:** Search files for lines matching regular expressions.

```bash
grep [options] "<pattern>" [path...]
```

| Option | Description |
|---|---|
| `-i` | Case-insensitive matching |
| `-r`, `-R` | Search directories recursively (`-R` follows symlinks) |
| `-n` | Print line numbers with output matches |
| `-v` | Invert match: select non-matching lines |
| `-c` | Count matching lines instead of printing content |
| `-l` | Print only filenames of files containing matches |
| `-E` | Extended regular expressions (equivalent to `egrep`, supports `+`, `?`, `|`, `()`) |
| `-C <n>` | Print `<n>` lines of context before and after match |
| `-A <n>` | Print `<n>` lines after match |
| `-B <n>` | Print `<n>` lines before match |

**Examples:**
```bash
# Search recursively for an error string across all files
grep -rn "DatabaseConnectionException" /var/www/backend/

# Filter active configuration settings (strip comments and blank lines)
grep -vE "^\s*#|^\s*$" /etc/nginx/nginx.conf

# Show 3 lines of surrounding context around an exception
grep -C 3 "NullPointerException" server.log
```

---

### `diff`
**Purpose:** Compare two files line-by-line and display differences.

```bash
diff [options] <file1> <file2>
```

| Option | Description |
|---|---|
| `-u` | Unified output format (standard Git-like patch format) |
| `-y` | Side-by-side comparison layout |
| `-w` | Ignore all whitespace differences |
| `-r` | Recursively compare subdirectories |

**Examples:**
```bash
# Generate unified diff comparison between original and edited config
diff -u /etc/ssh/sshd_config /etc/ssh/sshd_config.new

# Compare two directories to see modified and missing files
diff -qr /var/www/v1 /var/www/v2
```

---

### `wc`
**Purpose:** Print newline, word, character, and byte counts for files or standard input.

```bash
wc [options] [file...]
```

| Option | Description |
|---|---|
| `-l` | Count lines (newlines) |
| `-w` | Count words |
| `-c` | Count bytes |
| `-m` | Count characters (handles multi-byte UTF-8 correctly) |

**Examples:**
```bash
# Count total lines in a file
wc -l access.log

# Count number of running processes
ps aux | wc -l
```

---

## 4. Edit and Process Text

Command-line editors, text streaming utilities, and UNIX pipeline constructs.

### `nano`
**Purpose:** Simple, beginner-friendly modeless command-line text editor.

```bash
nano [options] <file>
```

**Common Shortcuts:**
- `Ctrl + O`: Write out (save) file.
- `Ctrl + X`: Exit editor (prompts to save if modified).
- `Ctrl + W`: Where is (search text).
- `Ctrl + K`: Cut line into buffer.
- `Ctrl + U`: Uncut (paste) buffered line.
- `Ctrl + _`: Jump to line number.

**Examples:**
```bash
# Edit a local configuration file
nano ~/.bashrc
```

---

### `vim`
**Purpose:** Powerful modal text editor for fast, keyboard-driven file editing.

```bash
vim <file>
```

**Essential Vim Modes and Operations:**
- **Normal Mode** (Default): Navigation and command execution.
  - Press `i` to enter **Insert Mode** (start typing).
  - Press `Esc` to return to **Normal Mode**.
- **Saving & Quitting** (from Normal Mode):
  - `:w` — Save file.
  - `:wq` or `ZZ` — Save and quit.
  - `:q!` — Quit immediately discarding all unsaved changes.
- **Editing & Navigation**:
  - `dd` — Delete (cut) current line.
  - `yy` — Yank (copy) current line.
  - `p` — Paste after cursor.
  - `u` — Undo last change.
  - `Ctrl + r` — Redo change.
  - `/text` — Search forward for text.

---

### `cut`
**Purpose:** Remove or extract specific columns and delimited fields from lines of text.

```bash
cut [options] [file]
```

| Option | Description |
|---|---|
| `-d "<delim>"` | Field delimiter character (default is Tab) |
| `-f <fields>` | List of field numbers to extract (e.g., `1`, `1,3`, `2-5`) |
| `-c <chars>` | Character position range to extract |

**Examples:**
```bash
# Extract usernames (field 1) from passwd file using colon delimiter
cut -d ":" -f 1 /etc/passwd

# Extract columns 1 and 3 from a comma-separated file
cut -d "," -f 1,3 data.csv
```

---

### `sort`
**Purpose:** Sort lines of text files in alphabetical, numerical, or custom order.

```bash
sort [options] [file...]
```

| Option | Description |
|---|---|
| `-n` | Compare according to numerical value |
| `-r` | Reverse sort order |
| `-k <col>` | Sort via a specific column key |
| `-u` | Output unique lines only (discard duplicate lines) |
| `-h` | Human-numeric sort (understands `2K`, `5M`, `1G`) |

**Examples:**
```bash
# Sort a list of IP addresses numerically
sort -n -t . -k 1,1 -k 2,2 -k 3,3 -k 4,4 ip_list.txt

# Sort disk consumption from du output in human-readable descending order
du -h --max-depth=1 /var | sort -hr
```

---

### `uniq`
**Purpose:** Filter out or report repeated adjacent lines from input.

> [!IMPORTANT]
> `uniq` only detects adjacent duplicate lines. You **must sort the input first** (`sort | uniq`) to eliminate all non-adjacent duplicates across the entire file.

```bash
uniq [options] [input [output]]
```

| Option | Description |
|---|---|
| `-c` | Prefix lines by the number of occurrences |
| `-d` | Print only duplicate lines |
| `-u` | Print only unique lines (lines that appeared exactly once) |
| `-i` | Ignore differences in case |

**Examples:**
```bash
# Count frequency of each unique visitor IP
awk '{print $1}' access.log | sort | uniq -c | sort -nr
```

---

### `tr`
**Purpose:** Translate, squeeze, or delete characters from standard input.

```bash
tr [options] <set1> [set2]
```

| Option | Description |
|---|---|
| `-d` | Delete characters in `set1` |
| `-s` | Squeeze repeats: replace multiple consecutive instances with a single character |

**Examples:**
```bash
# Convert text stream to all uppercase
echo "hello world" | tr 'a-z' 'A-Z'

# Remove Windows carriage returns (\r) from a text file
cat windows.txt | tr -d '\r' > linux.txt

# Squeeze multiple consecutive spaces into a single space
echo "foo    bar   baz" | tr -s ' '
```

---

### `sed`
**Purpose:** Stream editor for automated text parsing, filtering, and pattern replacement.

```bash
sed [options] '<command>' [file]
```

| Option | Description |
|---|---|
| `-i` | Edit files in place (modifies the file directly) |
| `-i.bak` | Edit file in place while saving a `.bak` backup file |
| `-e` | Specify multiple editing scripts |
| `-n` | Suppress automatic printing of pattern space |

**Basic Syntax:**
- Substitution: `s/search_pattern/replacement/g` (`g` = global flag on line).
- Deletion: `/pattern/d` (deletes lines matching pattern).

**Examples:**
```bash
# Replace 'localhost' with '127.0.0.1' across all lines in config.js
sed -i 's/localhost/127.0.0.1/g' config.js

# Delete all commented lines starting with #
sed '/^#/d' /etc/nginx/nginx.conf

# Print only lines 10 to 20 from a file
sed -n '10,20p' large_file.txt
```

---

### `awk`
**Purpose:** Pattern scanning, field extraction, and data formatting programming language.

```bash
awk [options] 'pattern { action }' [file]
```

| Variable / Option | Meaning |
|---|---|
| `-F "<delim>"` | Set input field separator (default: whitespace) |
| `$0` | The entire current line |
| `$1, $2, ...` | Specific field number 1, 2, etc. |
| `NR` | Current Record Number (line number) |
| `NF` | Number of Fields on current line |

**Examples:**
```bash
# Print username and shell from /etc/passwd
awk -F ":" '{print $1, $7}' /etc/passwd

# Print process ID and command name for processes using > 5% memory
ps aux | awk '$4 > 5.0 {print $2, $4, $11}'

# Calculate the sum of column 3 in a numbers file
awk '{sum += $3} END {print "Total:", sum}' data.txt
```

---

### Pipes and Redirection

Linux handles input and output using standard POSIX data streams:
- `stdin` (File Descriptor 0): Standard Input.
- `stdout` (File Descriptor 1): Standard Output.
- `stderr` (File Descriptor 2): Standard Error.

```bash
# 1. Pipe: Send stdout of cmd1 into stdin of cmd2
cmd1 | cmd2

# 2. Overwrite stdout to file
cmd > output.txt

# 3. Append stdout to file
cmd >> output.txt

# 4. Redirect stderr to file
cmd 2> error.log

# 5. Redirect both stdout and stderr to the same file
cmd &> combined.log
# (Alternative syntax): cmd > combined.log 2>&1

# 6. Discard all output silently (the black hole)
cmd > /dev/null 2>&1

# 7. Feed file content into stdin of command
cmd < input.txt
```

---

### Spotlight: `>` vs `>>`

| Operator | Action | Risk Factor | Safe Use Case |
|---|---|---|---|
| `>` | **Overwrites** the target file completely. If the file exists, it is truncated to 0 bytes first. | **High**: Overwriting an existing configuration file or database dump destroys previous data. | Creating a new file from scratch or resetting log files. |
| `>>` | **Appends** content to the end of the file. Existing content is left intact. | **Low**: Retains existing data and simply adds lines to the bottom. | Logging, adding keys to `~/.ssh/authorized_keys`, updating environment files. |

```bash
# DANGEROUS: Truncates ~/.bashrc to just this single line!
echo "export PATH=$PATH:/custom/bin" > ~/.bashrc

# SAFE: Appends the line without touching previous contents
echo "export PATH=$PATH:/custom/bin" >> ~/.bashrc
```

---

### `tee`
**Purpose:** Read from standard input and write to both standard output and files concurrently.

```bash
cmd | tee [options] <file...>
```

| Option | Description |
|---|---|
| `-a` | Append to the given file rather than overwriting |

**Examples:**
```bash
# View command progress on screen while saving to a log file
./deploy.sh | tee deployment.log

# Write to a root-owned file using sudo without opening an interactive editor
echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf
```

---

### `xargs`
**Purpose:** Build and execute command lines from standard input arguments.

```bash
cmd | xargs [options] [target_cmd]
```

| Option | Description |
|---|---|
| `-I <replace_str>` | Replace occurrences of `<replace_str>` with input item name |
| `-n <max-args>` | Use at most `<max-args>` arguments per command line execution |
| `-0` | Input items are terminated by a null character (essential for filenames with spaces) |
| `-P <max-procs>` | Run up to `<max-procs>` processes concurrently |

**Examples:**
```bash
# Find and delete files safely handling spaces in filenames
find . -name "*.bak" -print0 | xargs -0 rm -f

# Download multiple URLs in parallel using 4 worker threads
cat urls.txt | xargs -n 1 -P 4 curl -O
```

---

## 5. Monitor System Resources

Tools to assess system health, memory consumption, CPU performance, and disk usage.

### `top` / `htop`
**Purpose:** Real-time dynamic inspection of active system processes, CPU, and RAM allocation.

```bash
top
htop
```

**Common `top` Shortcuts:**
- `M`: Sort process table by Memory consumption (`%MEM`).
- `P`: Sort process table by CPU consumption (`%CPU`).
- `k`: Prompt for a PID to send a termination signal.
- `q`: Quit.

> [!TIP]
> `htop` is a modern, colored, interactive alternative to `top` featuring visual meters and mouse support. Install via package manager (`sudo apt install htop`).

---

### `free`
**Purpose:** Display total, used, and available physical RAM and swap space.

```bash
free [options]
```

| Option | Description |
|---|---|
| `-h` | Human-readable output (MB, GB automatic scaling) |
| `-m` | Display values in Megabytes |
| `-g` | Display values in Gigabytes |
| `-s <sec>` | Continuously display memory metrics every `<sec>` seconds |

**Understanding Memory Output:**
- **total:** Installed hardware memory.
- **used:** Memory allocated by processes.
- **free:** Completely unallocated memory.
- **buff/cache:** Memory used by kernel for filesystem buffers and page caching.
- **available:** **The most critical metric.** Estimated amount of memory available for starting new applications without swapping (includes reclaimable cache).

**Examples:**
```bash
# Check memory metrics in human units
free -h
```

---

### `uptime`
**Purpose:** Display how long the system has been running, logged-in users, and system load averages.

```bash
uptime
```

**Understanding Load Averages (`1 min`, `5 min`, `15 min`):**
- Load average represents the average number of threads in a runnable or uninterruptible state.
- On a system with **4 CPU cores**:
  - A load average of `4.0` means CPU cores are at 100% capacity.
  - A load average of `2.0` means CPU cores are at 50% capacity.
  - A load average of `8.0` means the system is overloaded; processes are queuing for CPU time.

---

### `vmstat`
**Purpose:** Report virtual memory, swap activity, disk I/O, process count, and CPU state.

```bash
vmstat [options] [delay [count]]
```

**Examples:**
```bash
# Sample system activity every 2 seconds for 5 iterations
vmstat 2 5
# Look at 'si' (swap in) and 'so' (swap out). High values indicate RAM starvation!
```

---

### `df`
**Purpose:** Report filesystem disk space usage and free storage availability.

```bash
df [options] [path]
```

| Option | Description |
|---|---|
| `-h` | Human-readable sizes (GB, MB) using powers of 1024 |
| `-T` | Print filesystem type (e.g., `ext4`, `xfs`, `btrfs`) |
| `-i` | Display **inode** information instead of block usage |

**Examples:**
```bash
# Check disk availability across all mounted partitions
df -hT

# Check inode consumption (solve "No space left on device" when disk shows free GB)
df -i
```

---

### `du`
**Purpose:** Estimate file space usage and folder directory sizes recursively.

```bash
du [options] [path...]
```

| Option | Description |
|---|---|
| `-s` | Summary mode: display only total size for each argument |
| `-h` | Human-readable sizes (KB, MB, GB) |
| `-d <n>` or `--max-depth=<n>` | Restrict recursion to `<n>` levels deep |

**Examples:**
```bash
# Check total size of current directory
du -sh .

# Identify largest directories in /var up to 1 level deep
du -h --max-depth=1 /var | sort -hr | head -n 10
```

---

### Spotlight: `df` vs `du`

| Feature | `df` (Disk Free) | `du` (Disk Usage) |
|---|---|---|
| **What it measures** | Filesystem superblock metadata. | Recursive disk blocks consumed by actual files. |
| **Speed** | Instantaneous O(1), regardless of disk size. | Slower O(N), must traverse the directory tree. |
| **Open Deleted Files** | **Includes** space held by deleted files still held open by running processes. | **Cannot see** deleted files because they no longer have directory entries. |

> [!NOTE]
> If `df` reports 99% full, but `du` only finds 50GB used on a 500GB disk, a running process (like a web server or database) is holding open a deleted log file. Identify it with: `lsof +L1` or `lsof | grep deleted`.

---

### `uname`
**Purpose:** Print kernel and operating system architecture details.

```bash
uname [options]
```

| Option | Description |
|---|---|
| `-a` | Print all system information (kernel name, network node, release, machine) |
| `-r` | Print kernel release version (e.g., `6.8.0-45-generic`) |
| `-m` | Print hardware architecture (e.g., `x86_64`, `aarch64`) |

**Examples:**
```bash
# Print complete kernel information
uname -a
```

---

### `lscpu`
**Purpose:** Gather and format CPU architecture details from `sysfs` and `/proc/cpuinfo`.

```bash
lscpu
```

**Examples:**
```bash
# View CPU cores, sockets, threads, and architecture
lscpu | grep -E "Model name|Socket|Thread|NUMA|CPU\(s\):"
```

---

### `lsblk`
**Purpose:** List information about all available block devices in a tree structure.

```bash
lsblk [options]
```

| Option | Description |
|---|---|
| `-f` | Output info about filesystems (FSTYPE, LABEL, UUID, Mountpoint) |
| `-m` | Output permission and owner details |

**Examples:**
```bash
# View disk partitions and mountpoints
lsblk -f
```

---

### `hostnamectl`
**Purpose:** Query and modify system hostname and related settings on systemd distros.

```bash
hostnamectl [status]
```

**Examples:**
```bash
# View operating system and kernel version
hostnamectl

# Change system hostname (requires root)
sudo hostnamectl set-hostname web-prod-01
```

---

## 6. Manage Processes and Services

Commands to track, kill, prioritize, and manage background services.

### `ps`
**Purpose:** Provide a snapshot of current running processes.

```bash
ps [options]
```

| Common Flag Combinations | Syntax Style | Description |
|---|---|---|
| `ps aux` | BSD Style | Displays all processes running across the system with user, CPU, memory, and command |
| `ps -ef` | POSIX Style | Full listing showing UID, PID, PPID (parent PID), and start time |

**Key Output Columns in `ps aux`:**
- `USER`: Process owner.
- `PID`: Process ID number.
- `%CPU` / `%MEM`: Percentage of CPU and RAM used.
- `STAT`: Process status (`R` = Running, `S` = Sleeping, `Z` = Zombie, `T` = Stopped, `D` = Uninterruptible sleep/disk wait).
- `COMMAND`: Program name and arguments.

**Examples:**
```bash
# Snapshot all processes and filter for python
ps aux | grep "[p]ython"

# List top 5 memory consuming processes
ps aux --sort=-%mem | head -n 6
```

---

### `pgrep` / `pidof`
**Purpose:** Look up process IDs based on program name or attributes.

```bash
pgrep [options] <pattern>
pidof <program_name>
```

| Option | Description |
|---|---|
| `-l` | List process name along with PID |
| `-u <user>` | Match only processes owned by `<user>` |
| `-f` | Match against full command line arguments, not just process name |

**Examples:**
```bash
# Find PIDs for all running nginx workers
pgrep -l nginx

# Find PID of exact binary
pidof mysqld
```

---

### `kill`
**Purpose:** Send signals to terminate or control processes by PID.

```bash
kill [options] <PID...>
```

| Signal Number | Signal Name | Behavior |
|---|---|---|
| `1` | `SIGHUP` | Hangup: Instructs daemons to reload configuration files without restart |
| `2` | `SIGINT` | Interrupt: Terminal interrupt signal (identical to pressing `Ctrl + C`) |
| `15` | `SIGTERM` | Terminate: **Default graceful shutdown request**. Lets process clean up |
| `9` | `SIGKILL` | Kill: **Forced immediate termination by kernel**. Process cannot catch or ignore |

**Examples:**
```bash
# Request graceful shutdown (Default SIGTERM 15)
kill 12345

# Forcefully kill an unresponsive process (SIGKILL 9)
kill -9 12345

# Instruct daemon to reload its configuration (SIGHUP 1)
sudo kill -HUP $(pidof nginx)
```

---

### Spotlight: `SIGTERM` (15) vs `SIGKILL` (9)

> [!IMPORTANT]
> **Always attempt `SIGTERM` (15) first.** `SIGTERM` allows the application to flush pending writes to disk, close database connections, release file locks, and clean up temporary sockets.
>
> Using `SIGKILL` (`kill -9`) preempts the application instantly at the kernel level without cleanup. This can corrupt open database files, leave locks unreleased, or orphan subprocesses. Reserve `kill -9` exclusively for processes stuck in infinite loops that refuse to respond to `SIGTERM`.

---

### `pkill` / `killall`
**Purpose:** Send signals to processes matching a name pattern.

```bash
pkill [options] <pattern>
killall [options] <exact_name>
```

| Option | Description |
|---|---|
| `-9` | Send `SIGKILL` rather than default `SIGTERM` |
| `-u <user>` | Terminate processes owned by a specific user |
| `-f` | Match full command line path and arguments |

**Examples:**
```bash
# Gracefully stop all node processes
pkill -15 -f "node"

# Kill all processes belonging to user 'testuser'
sudo pkill -u testuser
```

---

### Background Jobs
Manage processes run from the interactive shell session.

- `<cmd> &` — Run `<cmd>` in the background, freeing your terminal immediately.
- `nohup <cmd> &` — Run command immune to hangup signals (`SIGHUP`). Remains running if SSH disconnects.
- `Ctrl + Z` — Suspend (pause) current foreground process and place it in the background.
- `jobs -l` — List active background jobs and their PIDs.
- `bg %1` — Resume suspended job number 1 in the background.
- `fg %1` — Bring background job number 1 to the foreground.

**Examples:**
```bash
# Start a long-running batch job that survives terminal logout
nohup python3 run_pipeline.py > pipeline.log 2>&1 &
```

---

### `systemctl`
**Purpose:** Control the systemd system and service manager.

```bash
systemctl [command] [unit]
```

| Action | Description |
|---|---|
| `status <unit>` | Show active status, uptime, PID, and recent log snippets |
| `start <unit>` | Start an inactive service |
| `stop <unit>` | Stop a running service |
| `restart <unit>`| Stop then start a service |
| `reload <unit>` | Reload configuration without dropping client connections |
| `enable <unit>` | Configure service to start automatically on system boot |
| `disable <unit>`| Prevent service from starting on boot |
| `is-active <unit>`| Check if service is currently running (returns exit code 0 if active) |

**Examples:**
```bash
# Inspect status of PostgreSQL service
systemctl status postgresql

# Restart web server (requires root)
sudo systemctl restart nginx

# Enable Redis to launch automatically on server reboot
sudo systemctl enable redis-server
```

---

### `journalctl`
**Purpose:** Query and view system logs indexed by the systemd journal service.

```bash
journalctl [options]
```

| Option | Description |
|---|---|
| `-u <unit>` | Filter logs for a specific systemd service unit |
| `-f` | Follow logs in real time (live stream) |
| `-e` | Jump directly to the end of the log pager |
| `-n <count>` | Show the most recent `<count>` lines |
| `-p <level>` | Filter by log priority (e.g., `err`, `warning`, `info`) |
| `--since "<time>"` | Filter logs since a timestamp (e.g., `"1 hour ago"`, `"today"`) |
| `-b` | Show logs from the current boot only |

**Examples:**
```bash
# Tail nginx logs live
journalctl -u nginx -f

# View errors across the entire system from the current boot
journalctl -b -p err

# View logs generated in the last 30 minutes
journalctl --since "30 min ago"
```

---

## 7. Networking

Commands for configuring network interfaces, auditing open ports, diagnosing routes, and transferring files.

### `ip`
**Purpose:** Comprehensive modern tool for inspecting and configuring network interfaces, routing, and tunnels (replaces legacy `ifconfig`).

```bash
ip [options] <object> <command>
```

| Object | Description |
|---|---|
| `addr` (`a`) | Protocol addresses (IPv4 / IPv6) on devices |
| `route` (`r`)| Routing table entries |
| `link` (`l`) | Physical or virtual network devices and MAC addresses |

**Examples:**
```bash
# Show IP addresses for all interfaces
ip addr show

# Show IP addresses in compact, brief table format
ip -br a

# Display default gateway and kernel routing table
ip route show
```

---

### `ping`
**Purpose:** Test network reachability between hosts using ICMP ECHO packets.

```bash
ping [options] <host>
```

| Option | Description |
|---|---|
| `-c <count>` | Stop after sending `<count>` ECHO_REQUEST packets |
| `-i <interval>` | Wait `<interval>` seconds between sending packets |
| `-W <timeout>` | Time to wait for a response in seconds |

**Examples:**
```bash
# Test connection with exactly 4 packets
ping -c 4 8.8.8.8
```

---

### `traceroute` / `tracepath`
**Purpose:** Trace network route hops taken by packets across intermediate routers to a destination.

```bash
traceroute [options] <host>
tracepath <host>
```

**Examples:**
```bash
# Trace route to host (tracepath requires no root privileges)
tracepath 1.1.1.1

# Trace route using standard ICMP echo requests
traceroute -I google.com
```

---

### `ss`
**Purpose:** Socket statistics utility for investigating listening ports and network connections (faster, modern replacement for `netstat`).

```bash
ss [options]
```

| Option | Description |
|---|---|
| `-t` | Display TCP sockets |
| `-u` | Display UDP sockets |
| `-l` | Display listening sockets only (services waiting for connections) |
| `-p` | Show process name and PID using the socket (requires `sudo`) |
| `-n` | Do not resolve service names; show numeric ports (e.g., `80` instead of `http`) |
| `-a` | Show both listening and established sockets |

**Examples:**
```bash
# Inspect all listening TCP and UDP ports with process names
sudo ss -tulpn

# Show established TCP connections to HTTPS (port 443)
ss -tn state established '( dport = :443 or sport = :443 )'
```

---

### `lsof`
**Purpose:** List open files, sockets, and active network connections.

```bash
lsof [options]
```

| Option | Description |
|---|---|
| `-i [protocol][@host][:port]` | Filter network connections (e.g., `-i :80`, `-i tcp`) |
| `-u <user>` | List files and sockets opened by `<user>` |
| `-p <PID>` | List files and sockets opened by process ID `<PID>` |
| `+D <dir>` | Recursively list open file descriptors inside directory `<dir>` |

**Examples:**
```bash
# Identify which process is listening on port 8080
sudo lsof -i :8080

# Show all active network connections for user 'app'
sudo lsof -u app -i
```

---

### `curl`
**Purpose:** Transfer data to or from network servers using HTTP, HTTPS, FTP, and other protocols.

```bash
curl [options] <URL>
```

| Option | Description |
|---|---|
| `-I` | Fetch HTTP headers only (HEAD request) |
| `-o <file>` | Write response body to designated local `<file>` |
| `-O` | Write response to a file named after the remote URL file |
| `-L` | Follow HTTP redirects (301, 302) |
| `-s` | Silent mode: hide progress meter and error messages |
| `-v` | Verbose mode: display SSL handshake and request headers |
| `-X <method>`| Specify custom HTTP method (`GET`, `POST`, `PUT`, `DELETE`) |
| `-H "<header>"` | Send custom HTTP request header |
| `-d "<data>"` | Send HTTP POST data payload |

**Examples:**
```bash
# Check HTTP response headers and follow redirects
curl -IL https://google.com

# Download an installation script directly to a file
curl -fsSL https://get.docker.com -o get-docker.sh

# Send a JSON payload via POST
curl -X POST https://api.example.com/v1/auth \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"secret"}'
```

---

### `wget`
**Purpose:** Non-interactive command-line file downloader supporting resume and recursive downloads.

```bash
wget [options] <URL>
```

| Option | Description |
|---|---|
| `-O <file>` | Write documents to `<file>` name |
| `-c` | Resume a partially-downloaded file |
| `-q` | Quiet mode: turn off download output |
| `-b` | Go to background immediately after startup |

**Examples:**
```bash
# Resume an interrupted ISO download
wget -c https://releases.ubuntu.com/24.04/ubuntu-24.04-desktop-amd64.iso
```

---

### `nc`
**Purpose:** Arbitrary TCP/UDP connections and listeners (Netcat).

```bash
nc [options] [host] [port]
```

| Option | Description |
|---|---|
| `-z` | Zero-I/O mode: scan for listening daemons without sending data |
| `-v` | Verbose output |
| `-l` | Listen mode: wait for inbound connections |
| `-p <port>` | Specify local port to listen on |

**Examples:**
```bash
# Test if port 3306 on a remote database host is reachable
nc -zv db.internal.lan 3306

# Create a quick local port listener for debugging webhooks
nc -l -p 9000
```

---

## 8. Users and Permissions

Commands for user authentication, privilege escalation, and filesystem security boundaries.

### `whoami` / `id`
**Purpose:** Print effective user and group identities.

```bash
whoami
id [options] [user]
```

**Examples:**
```bash
# Print current active username
whoami

# View user ID (UID), group ID (GID), and all supplementary group memberships
id
# Output: uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu),27(sudo),4(adm)
```

---

### `who` / `w`
**Purpose:** Show who is logged on and what they are currently doing.

```bash
who
w
```

**Examples:**
```bash
# Display logged in users, terminals (pts/tty), idle times, and current CPU tasks
w
```

---

### `sudo`
**Purpose:** Execute commands with superuser (root) privileges or another specified user identity.

```bash
sudo [options] <command>
```

| Option | Description |
|---|---|
| `-i` | Simulate initial login as root: loads root's full environment and sets `cwd` to `/root` |
| `-u <user>` | Run command as `<user>` instead of root |
| `-l` | List permitted commands for the current user in `/etc/sudoers` |
| `-v` | Update credentials cache without executing a command |

> [!NOTE]
> **Why `sudo` is required:** Modifying system files (`/etc`, `/usr`), package registries, binding to ports below `1024`, and restarting services alter the shared operating system state. `sudo` logs commands for accountability and prevents accidental system alteration during ordinary terminal work.

---

### `su`
**Purpose:** Substitute user identity or open an interactive login shell.

```bash
su [options] [username]
```

**Examples:**
```bash
# Switch to user 'deploy' with their complete environment
su - deploy

# Switch to root account directly (requires root password)
su -
```

---

### Spotlight: `su` vs `sudo` vs `sudo -i`

| Command | Authentication Required | Target Environment | Best Practice |
|---|---|---|---|
| `su -` | **Root password**. | Clean root login environment (`/root`). | Discouraged on multi-admin servers; root password sharing is a security risk. |
| `sudo <cmd>` | **User's own password**. | Current user's environment; single command execution. | **Standard practice**: Minimum privilege, fully audited in security logs. |
| `sudo -i` | **User's own password**. | Clean root login environment (`/root`). | Use when executing multi-step administrative or maintenance workflows. |

---

### `chmod`
**Purpose:** Change file and directory access mode bits (permissions).

```bash
chmod [options] <mode> <file...>
```

#### Permission Architecture
- **Classes:** `u` (User/Owner), `g` (Group), `o` (Others), `a` (All).
- **Permissions:** `r` (Read = 4), `w` (Write = 2), `x` (Execute = 1).

| Octal Value | Binary | Representation | Meaning on Files | Meaning on Directories |
|---|---|---|---|---|
| `7` | `111` | `rwx` | Read, write, execute | Enter, list, and modify contents |
| `6` | `110` | `rw-` | Read and write | Read and modify directory table |
| `5` | `101` | `r-x` | Read and execute | Enter and list directory contents |
| `4` | `100` | `r--` | Read only | List filenames only (cannot `cd` into) |
| `0` | `000` | `---` | No permissions | Completely inaccessible |

**Standard Permissions:**
- Files: `644` (`rw-r--r--` — owner can edit, everyone can read).
- Scripts: `755` (`rwxr-xr-x` — owner can edit, everyone can run).
- Directories: `755` (`rwxr-xr-x` — owner can manage, everyone can browse).
- Private Keys: `600` (`rw-------` — owner only).

**Examples:**
```bash
# Make a shell script executable
chmod +x build.sh

# Secure an SSH private key
chmod 600 ~/.ssh/id_rsa

# Recursively set standard file and directory permissions safely
find /var/www/site -type d -exec chmod 755 {} +
find /var/www/site -type f -exec chmod 644 {} +
```

> [!CAUTION]
> **Anti-Pattern Warning:** Never run `chmod -R 777 /path` to solve permission errors. Granting full world-writable access to code or upload folders exposes your system to trivial arbitrary code execution. Fix ownership with `chown` instead!

---

### `chown`
**Purpose:** Change file and directory owner and group.

```bash
chown [options] <user[:group]> <file...>
```

| Option | Description |
|---|---|
| `-R` | Recursively change ownership through directories and subfiles |
| `-v` | Verbose mode: output every file modified |

**Examples:**
```bash
# Change owner to 'www-data' and group to 'www-data'
sudo chown -R www-data:www-data /var/www/html

# Change owner only, preserving existing group
sudo chown appuser /opt/app/server.js
```

---

### `chgrp`
**Purpose:** Change group ownership of files.

```bash
chgrp [options] <group> <file...>
```

**Examples:**
```bash
# Change group ownership to developers
sudo chgrp -R developers /opt/shared_workspace
```

---

### `umask`
**Purpose:** Set or display the default file creation permission mask.

```bash
umask [mode]
```

**How Umask Works:**
- Default permissions without mask: Files = `666`, Directories = `777`.
- A umask of `022` subtracts `022`:
  - Files created: `666 - 022 = 644` (`rw-r--r--`).
  - Directories created: `777 - 022 = 755` (`rwxr-xr-x`).

---

### `useradd` / `usermod` / `passwd`
**Purpose:** Manage user accounts and passwords.

```bash
useradd [options] <username>
usermod [options] <username>
passwd [options] [username]
```

**Examples:**
```bash
# Create a new user with a home directory and bash shell
sudo useradd -m -s /bin/bash developer

# Set or reset password for user
sudo passwd developer

# Add an existing user to the sudo administrative group
sudo usermod -aG sudo developer
```

---

## 9. Package Management

Install, remove, update, and search software repositories across major distributions.

### Package Manager Cross-Reference Table

| Action | Debian / Ubuntu (`apt`) | RHEL / Fedora (`dnf`) | Arch Linux (`pacman`) |
|---|---|---|---|
| **Update repository lists** | `sudo apt update` | `sudo dnf check-update` | `sudo pacman -Sy` |
| **Upgrade all packages** | `sudo apt upgrade -y` | `sudo dnf upgrade -y` | `sudo pacman -Syu` |
| **Install package** | `sudo apt install <pkg>` | `sudo dnf install <pkg>`| `sudo pacman -S <pkg>` |
| **Remove package** | `sudo apt remove <pkg>` | `sudo dnf remove <pkg>` | `sudo pacman -R <pkg>` |
| **Search package** | `apt search <term>` | `dnf search <term>` | `pacman -Ss <term>` |
| **Show package details** | `apt show <pkg>` | `dnf info <pkg>` | `pacman -Si <pkg>` |
| **Remove orphans** | `sudo apt autoremove` | `sudo dnf autoremove` | `sudo pacman -Rns $(pacman -Qdtq)` |

---

### `apt` (Debian, Ubuntu)
**Purpose:** Modern high-level package management CLI for Debian derivatives.

```bash
# Step 1: Refresh local package list from remote repositories
sudo apt update

# Step 2: Install security patches and software upgrades
sudo apt upgrade -y

# Install packages
sudo apt install -y nginx postgresql-client

# Purge a package including all its configuration files
sudo apt purge nginx

# Clean up unused dependencies left behind by removed packages
sudo apt autoremove -y
```

---

### `dnf` / `yum` (Fedora, RHEL, Rocky, Alma)
**Purpose:** Next-generation RPM package manager.

```bash
# Refresh and upgrade all system packages
sudo dnf upgrade --refresh -y

# Install development tools group
sudo dnf groupinstall "Development Tools"

# Search for a package
dnf search htop
```

---

### `pacman` (Arch Linux)
**Purpose:** Package manager utility for Arch Linux.

```bash
# Full system update and package database synchronization
sudo pacman -Syu

# Install package
sudo pacman -S git

# Remove package and its unused dependencies
sudo pacman -Rs apache
```

---

## 10. Archive and Compression

Package and compress directory structures for backups and data transfers.

### `tar`
**Purpose:** Tape archive utility for creating, inspecting, and extracting tarball archives (`.tar`, `.tar.gz`, `.tar.bz2`, `.tar.xz`).

```bash
tar [options] [archive-file] [target...]
```

| Key Flag | Description |
|---|---|
| `-c` | **Create** a new archive |
| `-x` | **Extract** files from an archive |
| `-t` | **List** / table of contents without extracting |
| `-v` | **Verbose**: list files being processed |
| `-f` | **File**: specifies the archive filename (must be directly before archive name) |
| `-z` | Filter through **gzip** (`.tar.gz`) |
| `-j` | Filter through **bzip2** (`.tar.bz2`) |
| `-J` | Filter through **xz** (`.tar.xz`) |
| `-C <dir>` | Extract into target directory `<dir>` instead of current directory |

**Examples:**
```bash
# Create a compressed gzip archive of a folder
tar -czvf project_backup.tar.gz /var/www/myproject

# Extract an archive into a specific target folder
tar -xzvf project_backup.tar.gz -C /opt/restored/

# List contents of an archive without extracting
tar -tzvf project_backup.tar.gz
```

---

### `gzip` / `gunzip`
**Purpose:** Compress or decompress single files using Lempel-Ziv coding (LZ77).

```bash
gzip [options] <file...>
gunzip <file.gz>
```

| Option | Description |
|---|---|
| `-d` | Decompress (equivalent to running `gunzip`) |
| `-k` | Keep original file (by default, `gzip` deletes the uncompressed source file) |
| `-9` | Maximum compression level (slower, smaller file) |

**Examples:**
```bash
# Compress a database dump file while keeping original
gzip -k dump.sql
# Produces: dump.sql.gz

# Decompress a .gz file
gunzip -k dump.sql.gz
```

---

### `zip` / `unzip`
**Purpose:** Package and compress files into standard cross-platform `.zip` archives.

```bash
zip [options] <archive.zip> <files...>
unzip [options] <archive.zip>
```

**Examples:**
```bash
# Zip a directory recursively
zip -r source_code.zip src/ package.json README.md

# Inspect ZIP contents without unpacking
unzip -l source_code.zip

# Unzip into a designated destination directory
unzip source_code.zip -d /tmp/extracted
```

---

## 11. Storage and Disks

Commands for partitioning, mounting, and verifying block storage devices and filesystems.

### `lsblk` / `blkid`
**Purpose:** Inspect block devices, partition tables, and filesystem UUIDs.

```bash
lsblk -f
sudo blkid
```

**Examples:**
```bash
# Identify disk layout, partition labels, and UUIDs
lsblk -f
```

---

### `findmnt`
**Purpose:** Find and display mounted filesystems in a tree view.

```bash
findmnt [options]
```

**Examples:**
```bash
# View all active mount points in a clean tree hierarchy
findmnt

# Check where a specific disk device is mounted
findmnt /dev/nvme0n1p1
```

---

### `mount` / `umount`
**Purpose:** Attach and detach storage filesystems to the directory hierarchy.

```bash
mount [options] <device> <mountpoint>
umount [options] <mountpoint|device>
```

| Option | Description |
|---|---|
| `-o ro` | Mount filesystem in read-only mode |
| `-o remount,...` | Remount an already-mounted filesystem with updated flags |
| `-l` (`umount`) | Lazy unmount: detach immediately from hierarchy, clean up references when free |

**Examples:**
```bash
# Mount an external storage partition
sudo mount /dev/sdb1 /mnt/external_disk

# Unmount cleanly
sudo umount /mnt/external_disk
```

> [!TIP]
> If `umount` reports **"device is busy"**, identify which processes are accessing it with: `lsof +f -- /mnt/external_disk` or `fuser -m /mnt/external_disk`.

---

### `fdisk`
**Purpose:** Manipulate disk partition tables (MBR and GPT).

> [!CAUTION]
> **Destructive Command Warning:** Modifying partition tables or writing changes with `w` in `fdisk` can destroy data partitions irreversibly. Always confirm the device identifier (`/dev/sda`, `/dev/nvme0n1`) before execution.

```bash
sudo fdisk [options] <device>
```

**Examples:**
```bash
# List partition table for all connected disks
sudo fdisk -l
```

---

### `dd`
**Purpose:** Low-level convert and copy raw disk blocks.

> [!CAUTION]
> **Extremely High Risk Warning:** Known colloquially as "Disk Destroyer". Pointing `of=` (Output File) to the wrong drive (e.g., `of=/dev/sda` instead of `/dev/sdb`) will overwrite your boot partition and filesystem without warning.

```bash
dd if=<input_file> of=<output_file> [options]
```

| Option | Description |
|---|---|
| `if=<path>` | Input file or device path |
| `of=<path>` | Output file or device path |
| `bs=<size>` | Block size for read/write operations (e.g., `bs=4M`) |
| `status=progress`| Print periodic transfer rate and volume status |

**Examples:**
```bash
# Flash an ISO image to a verified USB flash drive
sudo dd if=ubuntu.iso of=/dev/sdb bs=4M status=progress conv=fsync
```

---

## 12. Shell Productivity

Techniques to navigate command history, configure aliases, and manage shell environments.

### `history`
**Purpose:** Display and search the session's command history list.

```bash
history [options]
```

**History Expansions & Shortcuts:**
- `!!` — Re-execute the previous command (e.g., `sudo !!` after permission denied).
- `!$` — Re-use the last argument of the previous command.
- `!n` — Re-execute command line number `n` from `history`.
- `!string` — Re-execute the most recent command starting with `string`.
- `Ctrl + R` — Interactive reverse search through command history.

**Examples:**
```bash
# Forgot sudo on a root command
systemctl restart docker
# Output: Access denied
sudo !!
# Executes: sudo systemctl restart docker

# Make a directory and immediately enter it using !$
mkdir -p /var/www/newsite
cd !$
# Executes: cd /var/www/newsite
```

---

### Environment Variables
Manage shell variables passed down to child processes.

```bash
# Print all exported environment variables
env

# Export variable for the current session and child processes
export DATABASE_URL="postgres://localhost:5432/mydb"

# Read variable value
echo "$DATABASE_URL"

# Remove variable definition
unset DATABASE_URL
```

> [!NOTE]
> Variables defined with `export` exist only for the current shell session. To persist variables across reboots and logins, add them to `~/.bashrc` (for user sessions) or `/etc/environment` (for system-wide settings).

---

### Command Aliases
Create custom shortcuts for lengthy or frequently executed commands.

```bash
# Temporary alias in active shell
alias ll='ls -lah'
alias gs='git status'
alias myip='curl -s https://ifconfig.me'

# Remove an alias
unalias ll
```

---

## 13. Common Command Combinations

Practical, real-world terminal command pipelines for daily administration.

### Recipe 1: Find the 10 Largest Files on Disk
```bash
find / -type f -exec du -h {} + 2>/dev/null | sort -rh | head -n 10
```

### Recipe 2: Search Specific Errors in Live Log Streams
```bash
tail -f /var/log/nginx/error.log | grep --line-buffered -iE "denied|fatal|500"
```

### Recipe 3: Terminate All Runaway Processes Matching a Name
```bash
pgrep -f "worker.py" | xargs kill -15
```

### Recipe 4: Count Top 10 Visitor IP Addresses in Access Logs
```bash
awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -nr | head -n 10
```

### Recipe 5: Safely Find and Remove Temporary Files Older Than 30 Days
```bash
find /tmp/app_cache -type f -name "*.tmp" -mtime +30 -exec rm -f {} +
```

### Recipe 6: Inspect Which Process is Bound to Port 8080
```bash
sudo ss -tulpn | grep :8080
# or: sudo lsof -i :8080
```

### Recipe 7: Append Text to a Root-Protected File Without Opening an Editor
```bash
echo "nameserver 1.1.1.1" | sudo tee -a /etc/resolv.conf
```

---

## 14. Useful Keyboard Shortcuts

Boost your command-line efficiency with standard Bash/Readline shortcuts.

### Command Line Editing & Navigation
| Shortcut | Action |
|---|---|
| `Ctrl + A` | Move cursor to the **beginning** of the line |
| `Ctrl + E` | Move cursor to the **end** of the line |
| `Alt + F` | Move cursor forward one word |
| `Alt + B` | Move cursor backward one word |
| `Ctrl + U` | Cut (kill) text from cursor to the **beginning** of the line |
| `Ctrl + K` | Cut (kill) text from cursor to the **end** of the line |
| `Ctrl + W` | Cut (kill) the word immediately **before** the cursor |
| `Ctrl + Y` | Paste (yank) the most recently cut text back to the cursor |
| `Ctrl + L` | Clear terminal screen (equivalent to typing `clear`) |

### Process Control
| Shortcut | Action |
|---|---|
| `Ctrl + C` | Send `SIGINT` to terminate the active foreground process |
| `Ctrl + Z` | Send `SIGTSTP` to suspend/pause foreground process into background |
| `Ctrl + D` | Send `EOF` (End of File); exits the current shell or terminal session |
| `Ctrl + S` | Freeze terminal output scrolling |
| `Ctrl + Q` | Resume terminal output scrolling |

### History Navigation
| Shortcut | Action |
|---|---|
| `Ctrl + R` | Interactive reverse history search (type keyword to find previous commands) |
| `Ctrl + G` | Cancel history search and return to blank prompt |
| `Up Arrow` / `Down Arrow` | Cycle through previous / next command history entries |

---

## 15. Common Mistakes and Pitfalls

### 1. Glob Expansion with `rm -rf *`
If your current directory contains a file named `-rf` or if an unquoted variable is empty, catastrophic deletions happen.
```bash
# BAD: If $DIR is empty, this becomes rm -rf /*
rm -rf $DIR/*

# GOOD: Ensure the variable exists before removal
rm -rf "${DIR:?Variable empty}/"*
```

### 2. Overwriting Instead of Appending (`>` vs `>>`)
Accidentally using `>` truncates your target configuration file to zero bytes before writing. Always double-check redirection operators when modifying system configs like `~/.bashrc` or `/etc/hosts`.

### 3. Blanket `chmod -R 777`
Setting `777` on a directory grants read, write, and execute permissions to all local users and web services. In production, web servers should only have write permissions to specific asset or cache directories.

### 4. Forgetting that `uniq` Requires Sorted Input
Running `uniq` on unsorted files misses non-consecutive duplicates. Always pipe into `sort` first:
```bash
# CORRECT:
sort input.txt | uniq
```

### 5. Inode Exhaustion vs Disk Block Exhaustion
A disk can be 100% full even when `df -h` says there are hundreds of gigabytes free! This happens when millions of tiny 0-byte files exhaust the filesystem's total inode table. Check with:
```bash
df -i
```

### 6. Windows CRLF Line Endings Breaking Shell Scripts
Shell scripts edited in Windows often contain carriage return characters (`\r\n`). When run on Linux, this results in:
`bash: ./script.sh: /bin/bash^M: bad interpreter: No such file or directory`
Fix with:
```bash
sed -i 's/\r$//' script.sh
# or: dos2unix script.sh
```
