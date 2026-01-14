# Disk Management

Disk management is a critical skill for any SysAdmin. It involves monitoring how much 
space is left, identifying what is hogging the disk, and managing partitions or logical volumes.

In Linux, "everything is a file," and disks are no exception. 
They are represented as device files in the `/dev` directory.

## 1. Monitoring Disk Space

Before you run out of space and services start crashing, use these two essential commands:

| Command | Purpose | Admin's Note |
| :--- | :--- | :--- |
| `df -h` | **Disk Free.** Shows total space and usage for all mounted filesystems. | The `-h` (human-readable) flag turns bytes into GB/MB. |
| `du -sh [path]` | **Disk Usage.** Shows the size of a specific directory or file. | Use `du -sh *` to see which folder in your current directory is the largest. |

## 2. Identifying Large Files

When a disk is at 99%, you need to find the "space-eaters" quickly. 
This command is an admin favorite:

```bash
sudo du -ah /var/log | sort -rh | head -n 10
```

*This lists the **top 10 largest files/folders** in `/var/log`, sorted by size.*

## 3. Partitions and Filesystems

Before a disk can be used, it must be partitioned and formatted with a filesystem (like **Ext4** or **XFS**).

* **`lsblk`**: Lists all block devices (disks and partitions) in a tree-like format. 
This is the best way to see how your disks are laid out.
* **`fdisk -l`**: Displays detailed information about partition tables.
* **`blkid`**: Shows the **UUID** (Universally Unique Identifier) of your partitions—essential for permanent mounting.

## 4. Mounting Disks

Mounting is the process of attaching a formatted partition to a specific directory (a "mount point").

* **Temporary Mount:** `sudo mount /dev/sdb1 /mnt/data`
* **Permanent Mount:** You must add an entry to the **`/etc/fstab`** file. 
If you make a mistake here, the system may fail to boot, so always test with `sudo mount -a` after editing.

## 5. Logical Volume Management (LVM)

Most modern Linux servers use **LVM** instead of simple partitions. 
LVM acts as a flexible layer between the physical disk and the OS, allowing you to:

* Resize partitions while the system is running.
* Combine multiple physical disks into one large virtual pool.

**Basic LVM Workflow:**

1. **PV (Physical Volume):** The raw disk (`pvcreate`).
2. **VG (Volume Group):** The pool of space (`vgcreate`).
3. **LV (Logical Volume):** The "virtual partition" you format and use (`lvcreate`).
