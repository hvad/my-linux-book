# Permissions and Ownership

In Linux, security is built on the concept of **Permissions** and **Ownership**. 
Because Linux is a multi-user system, every file and directory has a specific owner and 
a set of rules defining who can read, write, or execute it.

As a SysAdmin, mastering this is non-negotiable—incorrect permissions are the #1 cause of 
"Access Denied" errors and security vulnerabilities.


## 1. The Three Tiers of Ownership

Every file is assigned to three categories:

1. **User (u):** The individual who owns the file (usually the creator).
2. **Group (g):** A collection of users with shared access.
3. **Others (o):** Everyone else on the system.

## 2. The Three Types of Permissions

When you run `ls -l`, you see a string like `-rwxr-xr--`. Here is what those letters mean:

| Permission | Symbol | Numeric | Action on File | Action on Directory |
| :--- | :--- | :--- | :--- | :--- |
| **Read** | `r` | **4** | View file contents. | List files inside (`ls`). |
| **Write** | `w` | **2** | Modify file contents. | Create/Delete files inside. |
| **Execute** | `x` | **1** | Run as a program/script. | Enter the directory (`cd`). |

---

## 3. Managing Ownership (`chown`)

To change who owns a file or which group it belongs to, use `chown` (Change Owner).

* **Change owner:** `sudo chown john report.txt`
* **Change owner and group:** `sudo chown john:developers report.txt`
* **Recursive (entire folder):** `sudo chown -R john:john /var/www/html`

## 4. Managing Permissions (`chmod`)

To change the rules, use `chmod` (Change Mode). You can use numbers (Octal) or symbols.

### The Octal Method (Fastest)

You add the numbers together for each tier:

* `7` (4+2+1) = Read, Write, and Execute.
* `6` (4+2) = Read and Write.
* `5` (4+1) = Read and Execute.
* `4` = Read only.

**Common Commands:**

* `chmod 755 script.sh` → Owner can do everything; Group/Others can only read and execute.
* `chmod 644 config.txt` → Owner can read/write; Group/Others can only read.
* `chmod 600 private.key` → Only the owner can read/write (standard for SSH keys).

### The Symbolic Method (Specific)

* `chmod +x script.sh` (Add **execute** permission for everyone)
* `chmod u-w file.txt` (Remove **write** for the **owner**)
* `chmod g+s directory/` (Set **Group ID** advanced admin trick)

---

## Admin's "Golden Rules"

1. **Principle of Least Privilege:** Never give `777` (full access to everyone) permissions 
to solve a problem. It’s a massive security risk. Find the specific group that needs access instead.
2. **The "x" on Directories:** If a user doesn't have `x` (execute) permission on a directory, 
they cannot `cd` into it, even if they have `r` (read) permission to see the files inside.
3. **Check yourself:** After changing permissions, always verify with `ls -l`.


