# File system hierarchy

In Linux, the file system doesn't use drive letters (like `C:` or `D:`).
Instead, everything is organized into a single tree structure starting from 
the **Root** directory, represented by a forward slash `/`.

For a SysAdmin, knowing this map is essential for locating configuration files, logs, and binaries quickly.

## Key Directories Reference

| Directory | Name | Purpose (The SysAdmin View) |
| :--- | :--- | :--- |
| `/` | **Root** | The base of the entire file system. |
| `/bin` | **Binaries** | Essential command binaries (e.g., `ls`, `cp`, `grep`). |
| `/boot` | **Boot** | Files needed to boot the system (Kernel, GRUB). |
| `/dev` | **Devices** | Hardware representation (e.g., `/dev/sda` for a disk). |
| `/etc` | **Etc** | **The Config Hub.** System-wide configuration files live here. |
| `/home` | **Home** | Personal directories for users (e.g., `/home/john`). |
| `/lib` | **Libraries** | Shared libraries essential for the binaries in `/bin`. |
| `/media` | **Media** | Mount point for removable media (USB sticks, CDs). |
| `/mnt` | **Mount** | Temporary mount point for filesystems. |
| `/opt` | **Optional** | Add-on software packages (manually installed apps). |
| `/proc` | **Processes** | Virtual filesystem providing kernel and process info. |
| `/root` | **Root Home** | The home directory for the `root` user (superuser). |
| `/run` | **Run** | Runtime data (IDs, sockets) since the last boot. |
| `/sbin` | **Sys Binaries** | Essential binaries for system administration (e.g., `iptables`). |
| `/tmp` | **Temporary** | Temporary files (often cleared on reboot). |
| `/usr` | **User** | User programs, libraries, and documentation. |
| `/var` | **Variable** | Files that change frequently, like **logs** (`/var/log`). |

## Important Paths for Daily Work

* **Configuring services:** Always look in `/etc/`. For example, SSH config is at `/etc/ssh/sshd_config`.
* **Checking errors:** Your best friend is `/var/log/`. Check `syslog` or `journald` here.
* **Checking System Stats:** Browse `/proc/meminfo` or `/proc/cpuinfo` to see hardware specs directly from the kernel.
* **Third-party Apps:** If you install something manually (like a specific database version), it often lands in `/opt`.

**Admin's Note:** If you see a directory named `sbin` (System Binaries), it usually contains 
commands that require `sudo` or root privileges to execute, unlike the regular `bin`.
