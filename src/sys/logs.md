# Logs Basics

In the world of System Administration, logs are your most important diagnostic tool. 
When a service fails, a user can't log in, or the system behaves strangely, 
the answer is almost always recorded in a log file.

## 1. Where the Logs Live

Historically, Linux logs were stored as plain text files in `/var/log`. While many applications 
still do this, modern Linux distributions (using `systemd`) now use a centralized, binary 
logging system called the **Journal**.

| Log File / Tool | Purpose |
| :--- | :--- |
| `/var/log/syslog` | General system messages (Debian/Ubuntu). |
| `/var/log/messages` | General system messages (RHEL/CentOS). |
| `/var/log/auth.log` | Authentication logs (logins, `sudo` usage). |
| `/var/log/apache2/` | Web server error and access logs. |
| **`journalctl`** | The command to query the modern system journal. |

## 2. Mastering `journalctl`

Since the Journal is binary, you cannot read it with `cat` or `vi`. 
You must use the `journalctl` command. As a Quick Reference, these are the only flags you really need:

* **View everything (starting with newest):** `journalctl -r`
* **Follow logs in real-time:** `journalctl -f` (Essential for watching a service as it starts).
* **Logs for a specific service:** `journalctl -u nginx`
* **Logs since the last boot:** `journalctl -b`
* **Filter by priority (Errors only):** `journalctl -p err..emerg`

## 3. Traditional Text Log Tools

If you are reading text files in `/var/log`, use these "Admin Classics" to find the needle in the haystack:

* **`tail -f /var/log/auth.log`**: Watch login attempts as they happen.
* **`grep "error" /var/log/syslog`**: Filter the log for a specific keyword.
* **`less /var/log/syslog`**: Open the log in a searchable viewer (Press `/` to search, `q` to quit).

## 4. Log Rotation

Logs grow quickly. To prevent your hard drive from filling up, Linux uses a utility called 
**logrotate**. It automatically compresses old logs (e.g., `syslog.1.gz`) and eventually deletes the oldest ones.

**Admin's Note:** If you see a "Disk Full" error, `/var/log` is the first place you should check. 
Look for massive log files that might indicate a service is stuck in an "error loop," spamming the disk with messages.

### Summary Checklist for Troubleshooting

1. **Check the service status:** `systemctl status [service]`
2. **Read the specific service logs:** `journalctl -u [service] -e` (The `-e` jumps to the end).
3. **Check global errors:** `journalctl -p 3 -xb` (Shows errors from the current boot).
