# Linux: System Administration

In your daily workflow, **System Administration** is the art of maintaining a healthy, 
secure, and performant environment. While a regular user cares about the interface, an 
Admin cares about the **plumbing**: the processes, the logs, and the underlying stability of the system.

This section moves beyond basic commands and into the **lifecycle of a server**.

## The "Golden Rule" of Administration

**Always have a way back.** Before editing a critical configuration file in `/etc`, always create a backup:

`cp config_file config_file.bak`

This simple habit is the difference between a 5-minute fix and a 5-hour outage. 
