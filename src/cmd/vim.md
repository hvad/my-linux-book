# Text Editing with Vim

In your daily life as a SysAdmin, **Vim** (Vi IMproved) is an essential skill. 
While `nano` is friendly for beginners, Vim is available on almost every Linux server in 
existence even in "minimal" installations where other editors aren't present.

Vim is a **modal** editor, meaning keys do different things depending on which "mode" you are in.


## 1. The Three Essential Modes

To use Vim effectively, you must understand how to switch between these three states:

* **Normal Mode:** The default mode for navigating and deleting text. You cannot type regular text here. (Press `Esc` to return here).
* **Insert Mode:** Used for typing text. (Press `i` from Normal mode to enter).
* **Command Mode:** Used for saving, quitting, and advanced functions. (Type `:` from Normal mode)

## 2. The Survival Commands

If you get stuck in Vim, remember these steps: Press `Esc` multiple times, then type one of the following:

| Command | Action |
| :--- | :--- |
| `:w` | **Write** (Save) the file. |
| `:q` | **Quit** the editor. |
| `:wq` | **Save and Quit** (The most common way to exit). |
| `:q!` | **Force Quit** without saving changes. |
| `:set number` | Show line numbers (very helpful for debugging configs). |

## 3. Navigation and Editing (Normal Mode)

As an admin, you often need to jump to a specific line or delete a configuration error quickly. 
Use these shortcuts in **Normal Mode**:

* **`x`**: Delete a single character.
* **`dd`**: Delete (cut) the **entire line**.
* **`yy`**: Yank (copy) the current line.
* **`p`**: Paste the copied/cut line below.
* **`u`**: Undo the last action.
* **`/keyword`**: Search for a specific word in the file (Press `n` to find the next match).
* **`G`**: Jump to the **bottom** of the file.
* **`gg`**: Jump to the **top** of the file.


## Admin's Note: The "Vim-is-Everywhere" Rule

You might prefer a GUI editor, but when you are SSH into a broken server that only boots into a 
terminal, **Vim** will be your only way to fix the configuration files.

