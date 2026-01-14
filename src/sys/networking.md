# Networking Basics

Networking is what allows your Linux system to communicate with the world. 
As a SysAdmin, you need to know how to verify your IP address, check if a remote server 
is alive, and see which services are listening for connections.


## 1. Identifying Your Interface

In Linux, every network card (Ethernet, Wi-Fi, or Virtual) is an **interface**.

* **`lo`**: The "Loopback" interface (your own machine, `127.0.0.1`).
* **`eth0`** or **`enp3s0`** : Typical names for wired Ethernet.
* **`wlan0`**: Typical name for Wi-Fi.

| Task | Command | Admin's Note |
| :--- | :--- | :--- |
| **Check IP Address** | `ip addr` | Look for the `inet` line under your active interface. |
| **Check Routing** | `ip route` | Shows your **Default Gateway** (how you get to the internet). |
| **Link Status** | `ip link` | Shows if the "cable" is logically plugged in (`UP` or `DOWN`). |

## 2. Testing Connectivity

When a user says "the internet is down," use these tools to find where the connection is breaking.

* **`ping [IP/Domain]`**: Sends a tiny packet to see if a host is reachable.
* **`traceroute [Domain]`**: Shows every "hop" (router) your packet takes to reach its destination. 
Great for finding where a connection is being blocked.
* **`dig [Domain]`**: The primary tool for troubleshooting **DNS**. It tells you what IP address a domain name points to.

## 3. Ports and Listening Services

A server can run many services (Web, SSH, Database). Each one listens on a specific **Port**.

| Service | Port | Protocol |
| :--- | :--- | :--- |
| **SSH** | 22 | TCP |
| **HTTP** | 80 | TCP |
| **HTTPS** | 443 | TCP |
| **DNS** | 53 | UDP/TCP |

**How to see what's open:**

```bash
sudo ss -tulpn
```

* `-t`: TCP ports
* `-u`: UDP ports
* `-l`: Listening ports
* `-p`: Show the **Process** (program) using the port
* `-n`: Show numeric ports (e.g., `80` instead of `http`)

## 4. The "Old vs. New" Commands

Linux networking commands have transitioned over the years. You might see old tutorials 
using "deprecated" tools. It is best to use the newer **iproute2** suite.

| Old Tool (Deprecated) | New Tool (Preferred) |
| :--- | :--- |
| `ifconfig` | `ip addr` |
| `route` | `ip route` |
| `netstat` | `ss` |
| `arp` | `ip neighbor` |

### Admin's Summary: The "Can't Connect" Checklist

1. **Can I ping myself?** `ping 127.0.0.1` (Tests the network stack).
2. **Can I ping the gateway?** (Tests the local network/cable).
3. **Can I ping 8.8.8.8?** (Tests the internet connection).
4. **Is the service listening?** `sudo ss -tulpn | grep :80`.
