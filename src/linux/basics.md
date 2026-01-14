# Linux basic

To manage a Linux system efficiently, you only need to understand three fundamental pillars.

These govern almost every interaction you will have with the server.

1. Everything is a File

In Linux, almost everything from a simple text document to your hard drive and even your 
CPU is represented as a file.

- Hardware? Represented as files in /dev.

- System Settings? Managed via text files in /etc.

- Kernel Info? Accessed via files in /proc.

SysAdmin Tip: Because everything is a file, you can use the same tools (cat, grep, vi) 
to configure a service as you do to read a note.

2. The File System Hierarchy (FHS)Linux does not use drive letters (C:, D:). 

Everything exists under the Root directory (/).

| Directory | Purpose |
| :--- | :--- |
| /etc      | Configuration. Where you edit service settings (e.g., ssh, httpd). |
| /var/log  | Logs. The first place to look when something breaks. |
| /home     | Users. Where personal files and local configs reside. |
| /tmp      | Temporary. Files here are usually cleared on reboot. |
| /root     | The God User. The home directory for the system administrator. |

3. The Power of the Pipe (|) Linux is built on small, modular tools that do one thing well.
You combine them using the "Pipe." The output of one command becomes the input of the next.

Example:
```Bash
history | grep "ssh"
```
This doesn't just show your history; it filters it instantly to find every time you used SSH.
