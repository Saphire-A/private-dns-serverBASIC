# Step 02 – DNSMasq Installation

## Objective  
Install the `dnsmasq` service on Ubuntu. It will act as a **lightweight DNS forwarder** for the private DNS server.

---

## Installation Commands

```bash
sudo apt update
sudo apt install dnsmasq
```

✅ Verifying Installation
Method 1 – Using ps
```bash
ps aux | grep dnsmasq
```
Example Output:
```yaml
dnsmasq     1483  0.0  0.0  25740  3108 ?        S    17:38   0:00 /usr/sbin/dnsmasq ...
practice    4105  0.0  0.0  17812  2208 pts/0    S+   19:39   0:00 grep --color=auto dnsmasq
```

🔍 Method 2 – Using systemctl
```bash
sudo systemctl status dnsmasq
```
Expected Output:
```yaml
● dnsmasq.service - dnsmasq - A lightweight DHCP and caching DNS server
     Loaded: loaded (/usr/lib/systemd/system/dnsmasq.service; enabled; preset: enabled)
     Active: active (running) since Fri 2025-06-20 17:38:41 IST; ...
     ...
Jun 20 17:38:41 practice-VirtualBox dnsmasq[1483]: started, version 2.90 cachesize 150
Jun 20 17:38:41 practice-VirtualBox dnsmasq[1483]: DNS service limited to local subnets
Jun 20 17:38:41 practice-VirtualBox dnsmasq[1483]: read /etc/hosts - 8 names
⚠️ Note: Warnings about resolvconf or systemd-resolved can usually be ignored unless you're doing advanced DNS integration.

📡 Verifying DNS Port 53
Check if dnsmasq is listening on the standard DNS port (53):

```bash
sudo lsof -i :53
```
Expected Output:

```yaml
COMMAND  PID    USER     FD   TYPE  DEVICE SIZE/OFF NODE NAME
dnsmasq  1424   dnsmasq   4u  IPv4  ...    ...      UDP *:domain
dnsmasq  1424   dnsmasq   5u  IPv4  ...    ...      TCP *:domain (LISTEN)
dnsmasq  1424   dnsmasq   6u  IPv6  ...    ...      UDP *:domain
dnsmasq  1424   dnsmasq   7u  IPv6  ...    ...      TCP *:domain (LISTEN)
```
This confirms that dnsmasq is actively listening for both IPv4 and IPv6 requests via UDP and TCP.

Checking for Conflicts – systemd-resolved
Sometimes, systemd-resolved can interfere with dnsmasq by occupying port 53.

Check its status:
```bash
sudo systemctl status systemd-resolved
```
Ideal Result:

```yaml
● systemd-resolved.service - Network Name Resolution
     Loaded: loaded (...)
     Active: inactive (dead)
```
If it's inactive, you're good to go.

If it's active, disable it using:

```bash
sudo systemctl stop systemd-resolved
sudo systemctl disable systemd-resolved
```