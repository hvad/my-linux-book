# Basic Commands (ls, cd, pwd)

In your daily SysAdmin life, these three commands are your "eyes and legs."
You will use them thousands of times to navigate servers.

Here is the quick reference for **Navigation Basics**.


## Navigation: `pwd`, `ls`, and `cd`

### 1. `pwd` (Print Working Directory)

When you are deep in a nested directory structure, it’s easy to get lost. 
`pwd` tells you exactly where you are located.

* **Usage:** `pwd`
* **Why it matters:** Always run this before executing a destructive command 
like `rm -rf *` to ensure you are in the right place.

### 2. `ls` (List)

This command shows you what is inside a directory. As an admin, you rarely use `ls` alone 
you use **flags** to see the "truth" of the filesystem.

| Command | Result |
| :--- | :--- |
| `ls` | Basic list of visible files. |
| `ls -l` | **Long format.** Shows permissions, owner, size, and last modified date. |
| `ls -a` | **All files.** Shows hidden files (those starting with a `.`), like `.bashrc`. |
| `ls -lh` | **Human Readable.** Shows file sizes in KB, MB, or GB instead of bytes. |
| `ls -t` | **Time.** Sorts files by newest first (great for finding recent logs). |

**The "Admin Favorite":**

```bash
ls -altr
```

*This lists **a**ll files in **l**ong format, sorted by **t**ime, in **r**everse (newest files appear at the bottom of your screen).*

### 3. `cd` (Change Directory)

Moving between folders. Mastering `cd` is about using shortcuts to avoid typing long paths.

| Command | Destination |
| :--- | :--- |
| `cd /etc` | Move to an **absolute path** (starts from root `/`). |
| `cd ssh` | Move to a **relative path** (inside your current folder). |
| `cd ..` | Move **one level up** (to the parent directory). |
| `cd ~` | Go straight to your **Home** directory. |
| `cd -` | Go back to the **previous directory** you were in (toggle). |


### Tips for Speed

* **Tab Completion:** Never type a full directory name. Type the first few letters and hit `Tab`. 
If it doesn't complete, you either made a typo or there are multiple matches (hit `Tab` twice to see them).
* **Clear the noise:** If your terminal gets too cluttered with `ls` output, use the shortcut `Ctrl + L` 
to clear the screen without losing your command history.

