# Ssh Basics

Secure Shell (**SSH**) is the lifeblood of remote Linux administration. 
Because it provides a direct gateway to your server, it is also the primary target for brute-force attacks.

Hardening your SSH configuration is one of the first tasks you should perform on any new server.

## 1. The Configuration File

All SSH server settings are stored in a single text file. Always make a backup before editing:

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
sudo nano /etc/ssh/sshd_config
```

## 2. Critical Hardening Steps

To apply these changes, find the corresponding line in `sshd_config`, 
uncomment it (remove the `#`), and set the value as shown:

| Setting | Recommendation | Why it matters |
| :--- | :--- | :--- |
| **PermitRootLogin** | `no` | Prevents attackers from targeting the `root` account directly. |
| **PasswordAuthentication** | `no` | **Crucial.** Forces the use of SSH Keys, making brute-force impossible. |
| **PubkeyAuthentication** | `yes` | Allows login via secure cryptographic keys. |
| **Port** | `2222` (example) | Changing from default `22` reduces noise from automated bot scans. |
| **MaxAuthTries** | `3` | Limits the number of failed login attempts per connection. |
| **AllowUsers** | `john admin` | Only specific users listed here can log in via SSH. |

## 3. Using SSH Keys (The Pro Way)

Instead of typing a password, you use a **Public/Private key pair**. The private key stays 
on your laptop; the public key goes on the server.

**Step 1: Generate keys on your local machine**

```bash
ssh-keygen -t ed25519
```

**Step 2: Copy the public key to the server**

```bash
ssh-copy-id user@server-ip
```

## 4. Applying Changes

After editing the config file, you **must** restart the service for changes to take effect.

**Warning:** Always keep your current terminal session open while testing the new config in 
a *second* window. If you made a mistake, you won't be locked out.

```bash
sudo sshd -t          # Test syntax for errors first
sudo systemctl restart ssh
```

---

### Admin's Note: Fail2Ban

Even with a hardened config, bots will still try to connect. I highly recommend installing 
**Fail2Ban**. It monitors your logs and automatically bans any IP address that shows suspicious 
behavior (like 10 failed logins in one minute).

```bash
sudo apt install fail2ban  # Debian/Ubuntu
sudo dnf install fail2ban  # RHEL/Fedora
```
