# Linux: SysAdmin cheatsheet

Here is the comprehensive **Linux System Administration Quick Reference** compiled into a single structured guide.

## 1. Introduction to SysAdmin

System Administration is the art of maintaining the "plumbing" of a server. 
Your goals are **Observability** (knowing what's happening), **managing access** , 
and **Automation** (reducing manual tasks).

**The Golden Rule:** Always backup a config file before editing it:
`cp file.conf file.conf.bak`

## 2. The Command Line & Navigation

The CLI is your control center. It consists of the **Terminal** (the window) and 
the **Shell** (the program interpreting commands, like `bash`).

### Essential Navigation

* **`pwd`**: Print Working Directory (Where am I?).
* **`ls -altr`**: List all files, long format, sorted by time (newest at bottom).
* **`cd -`**: Toggle back to the previous directory.
* **`Tab`**: Auto-complete commands and paths.

## 3. Permissions and Ownership

Linux uses a three-tier permission system: **User (u)**, **Group (g)**, and **Others (o)**.

### The Numeric Method (`chmod`)

* **7 (rwx)**: Full access.
* **6 (rw-)**: Read and write.
* **5 (r-x)**: Read and execute.
* **4 (r--)**: Read only.

**Common Commands:**

* `chown user:group file`: Change ownership.
* `chmod 644 file`: Standard for data files.
* `chmod 755 script.sh`: Standard for executable scripts.

## 4. Package Management

Managing software depends on your distribution "family."

| Task | **APT** (Ubuntu/Debian) | **DNF** (RHEL/CentOS/Fedora) |
| :--- | :--- | :--- |
| **Install** | `sudo apt install [pkg]` | `sudo dnf install [pkg]` |
| **Update List** | `sudo apt update` | (Automatic) |
| **Upgrade All** | `sudo apt upgrade` | `sudo dnf upgrade` |
| **Remove** | `sudo apt remove [pkg]` | `sudo dnf remove [pkg]` |

## 5. Text Editing with Vim

Vim is a modal editor available on almost every server.

* **Insert Mode**: Press `i` to type.
* **Normal Mode**: Press `Esc` to navigate or delete (`dd` for line, `u` for undo).
* **Command Mode**: Type `:` from Normal mode.
* `:wq` (Save and quit)
* `:q!` (Quit without saving)

**Pro Tip:** Use the **amix/vimrc** configuration for a powerful setup:

```bash
git clone --depth=1 https://github.com/amix/vimrc.git ~/.vim_runtime
sh ~/.vim_runtime/install_awesome_vimrc.sh
```

## 6. Users and Processes

* **Users**: Data stored in `/etc/passwd`. Manage with `useradd` and `usermod`.
* **Processes**: Programs in execution.
* **`htop`**: Best interactive monitor for CPU/RAM.
* **`ps aux`**: Static snapshot of all processes.
* **`kill -9 [PID]`**: Forcefully stop a process.

## 7. Networking & Logs

* **Network**: Use `ip addr` to check IPs and `ss -tulpn` to see listening ports.
* **Logs**: The modern standard is `journalctl`.
* `journalctl -u [service] -f`: Follow specific service logs in real-time.
* `journalctl -p err -b`: Show all errors since last boot.

## 8. Disk Management

* **`df -h`**: Check overall disk space.
* **`du -sh *`**: Check size of folders in current directory.
* **`lsblk`**: View disk partitions and mount points.

### Final Troubleshooting Checklist

1. **Check Resources**: `top`, `free -h`, `df -h`.
2. **Check Logs**: `journalctl -xe`.
3. **Check Service**: `systemctl status [name]`.
4. **Check Network**: `ss -tulpn`.
