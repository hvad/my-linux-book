# Package Management

Software management is a cornerstone of system administration. On Linux, we rarely download `.exe` 
installers from websites; instead, we use **Package Managers** to fetch software from trusted repositories.

As an admin, you'll likely work with two main "families": 
**Debian-based** (using `.deb` files) and **Red Hat-based** (using `.rpm` files).


## 1. The Low-Level vs. High-Level Tools

Think of package management in two layers:

* **Low-Level Tools (`rpm`, `dpkg`):** These handle the actual installation of a local file. 
They do **not** resolve dependencies (if your app needs a library that isn't installed, these tools will simply fail).
* **High-Level Tools (`apt`, `dnf`):** These are the "smart" managers. They talk to the internet, 
find the software you want, and automatically download every dependency needed to make it work.

## 2. The APT Family (Debian, Ubuntu, Kali)

**APT** (Advanced Package Tool) manages `.deb` packages. It is known for its speed and human-readable output.

| Action | Command |
| :--- | :--- |
| **Update repo index** | `sudo apt update` |
| **Install a package** | `sudo apt install [package]` |
| **Upgrade all software** | `sudo apt upgrade` |
| **Search for a package** | `apt search [keyword]` |
| **Remove (keep configs)** | `sudo apt remove [package]` |
| **Purge (remove configs)** | `sudo apt purge [package]` |

**Admin's Note:** Always run `apt update` before `apt install` to ensure you are getting the latest 
version metadata from the servers.

## 3. The DNF Family (RHEL, Fedora, Rocky, Alma)

**DNF** (Dandified YUM) is the successor to the older `yum` tool. It manages `.rpm` packages and is 
highly regarded for its advanced dependency resolution and "history" feature.

| Action | Command |
| :--- | :--- |
| **Install a package** | `sudo dnf install [package]` |
| **Upgrade all software** | `sudo dnf upgrade` |
| **Search for a package** | `dnf search [keyword]` |
| **Remove a package** | `sudo dnf remove [package]` |
| **View history** | `dnf history` |
| **Rollback a change** | `sudo dnf history undo [ID]` |

**Admin's Note:** One of DNF's best features is `dnf history`. If an update breaks your system, 
you can literally "undo" that specific transaction.


## 4. Direct Comparison Cheatsheet

If you are switching between Ubuntu and CentOS/RHEL, use this table to translate your "muscle memory."

| Task | **APT** (Debian/Ubuntu) | **DNF** (RHEL/Fedora) |
| :--- | :--- | :--- |
| **Search** | `apt search [app]` | `dnf search [app]` |
| **Install** | `sudo apt install [app]` | `sudo dnf install [app]` |
| **Update Lists** | `sudo apt update` | (Handled automatically) |
| **Full Upgrade** | `sudo apt upgrade` | `sudo dnf upgrade` |
| **Show Info** | `apt show [app]` | `dnf info [app]` |
| **Clean Cache** | `sudo apt clean` | `sudo dnf clean all` |
| **Find what owns a file** | `dpkg -S /path/to/file` | `dnf provides /path/to/file` |


## 5. When to use `rpm` directly?

You use the low-level `rpm` command when you have a specific `.rpm` file on your disk that isn't in a repository.

* **Install a local file:** `rpm -ivh package.rpm`
* **Query if a package is installed:** `rpm -q package_name`
* **Verify integrity:** `rpm -V package_name` (Check if files have been modified since install).

**Admin's Warning:** Whenever possible, use `dnf install ./package.rpm` instead of `rpm -i`. 
DNF will attempt to find the dependencies online, whereas `rpm` will simply stop and complain if they are missing.

