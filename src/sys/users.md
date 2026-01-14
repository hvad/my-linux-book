# Users and Groups

In a multi-user environment like Linux, security and organization rely on **Users** and **Groups**. 
As an administrator, your job is to ensure users have enough access to do their work, 
but not enough to accidentally (or intentionally) damage the system.


## 1. Types of Users

Every process on Linux is "owned" by a user. There are three main types:

* **Root User:** The "Superuser" with UID 0. This user has unrestricted access to the entire system.
* **System Users:** Accounts created to run specific services (like `www-data` for web servers 
or `mysql` for databases). They usually cannot log in.
* **Regular Users:** Real people who log in to use the system. Their UIDs typically start at 1000.

## 2. The Power of Groups

Groups are collections of users. Instead of giving 10 people permission to a folder individually, 
you create a group, give the group permission, and add the users to it.

* **Primary Group:** Every user has exactly one primary group (usually named after themselves).
* **Secondary Groups:** Users can belong to many other groups to gain specific access 
(e.g., the `sudo` group to run admin commands or the `docker` group to manage containers).

## 3. Essential Management Commands

| Action | Command | Admin's Note |
| :--- | :--- | :--- |
| **Create User** | `sudo useradd -m [username]` | Use `-m` to create their home directory. |
| **Set Password** | `sudo passwd [username]` | Use this to reset forgotten passwords too. |
| **Delete User** | `sudo userdel -r [username]` | `-r` removes their files—use with caution! |
| **Create Group** | `sudo groupadd [group]` | Keep group names lowercase and simple. |
| **Add User to Group** | `sudo usermod -aG [group] [user]` | **Crucial:** Always use `-a` (append), or you'll kick them out of all other groups! |

## 4. Where the Data Lives

As a SysAdmin, you should know these three plain-text files:

1. **`/etc/passwd`**: Contains user account information (login name, UID, home directory).
2. **`/etc/group`**: Lists all groups and the users belonging to them.
3. **`/etc/shadow`**: Stores encrypted passwords. Only `root` can read this file.

### The "Sudo" Privilege

On modern systems, we rarely log in as `root` directly. Instead, we use `sudo` (SuperUser DO).

* **Audit Trail:** `sudo` logs every command run, providing a paper trail of who changed what.
* **The Sudoers File:** Managed via the `visudo` command. Never edit `/etc/sudoers` with a 
normal text editor; `visudo` checks for syntax errors before saving to prevent you from being locked out of your own system.

