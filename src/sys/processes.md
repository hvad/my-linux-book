# Process Management

Managing processes allows you to keep the system responsive. Think of this as the "Task Manager" 
of the Linux world, but much more granular.

## 1. Viewing Active Processes

| Command | Purpose | Admin's Note |
| :--- | :--- |: --- |
| `top` | **Real-time monitor.** The classic way to see CPU/RAM usage. | Press `q` to exit, `M` to sort by Memory, `P` to sort by CPU. |
| `htop` | **Interactive monitor.** A modern, colorized version of `top`. | Much easier to read. Use the mouse or function keys to kill processes. |
| `ps aux` | **Static snapshot.** Shows every process running on the system. | Use `ps aux` |

## 2. Identifying a Process (The PID)

Every process is assigned a unique **Process ID (PID)**. You need this number to act on the process.

* **Find a PID by name:** `pgrep httpd`
* **See parent/child relationships:** `pstree -p`

## 3. Terminating Processes (`kill`)

When a program freezes or consumes too many resources, you need to stop it. We do this by sending "signals."

* **The Polite Way (SIGTERM):** `kill [PID]`
Asks the program to save its data and close nicely.

* **The Forceful Way (SIGKILL):** `kill -9 [PID]`
Immediately kills the process. Use this only if the polite way fails.

* **Kill by Name:** `killall firefox` or `pkill -u [username]`

## 4. Background and Foreground

Sometimes you want to run a command but keep using your terminal.

* **Run in background:** Add `&` to the end (e.g., `cp -r /large_folder /backup &`).
* **See background jobs:** Type `jobs`.
* **Bring to foreground:** Type `fg %[job_number]`.

### Admin's Summary Table: Monitoring Health

| If you want to see... | Use this command: |
| :--- | :--- |
| **Overall System Uptime** | `uptime` |
| **Free Memory/RAM** | `free -h` |
| **Disk Usage** | `df -h` |
| **Live Disk I/O** | `iostat` (or `iotop`) |

**Admin's Note:** If a server is lagging, check the **Load Average** in `top`. If the numbers are 
significantly higher than the number of CPU cores you have, the system is bottlenecked and you need 
to find the offending PID immediately.
