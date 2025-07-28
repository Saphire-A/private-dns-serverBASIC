# Step 02 – DNSMasq Installation

#  Objective
To install the `dnsmasq` service on Ubuntu which will act as our lightweight DNS forwarder for the private DNS server.

---

# Commands Used

```bash
sudo apt update
sudo apt install dnsmasq
````

---

## Example Output – Check if `dnsmasq` is Running

You can verify that `dnsmasq` is running using either of the following:

### Method 1 – Using `ps`:

---bash
ps aux | grep dnsmasq


**Example Output:**

dnsmasq     1483  0.0  0.0  25740  3108 ?        S    17:38   0:00 /usr/sbin/dnsmasq ...
practice    4105  0.0  0.0  17812  2208 pts/0    S+   19:39   0:00 grep --color=auto dnsmasq

### Method 2 – Using `systemctl`:

```bash
sudo systemctl status dnsmasq
```

**Expected Output:**

```
● dnsmasq.service - dnsmasq - A lightweight DHCP and caching DNS server
     Loaded: loaded (/usr/lib/systemd/system/dnsmasq.service; enabled; preset: enabled)
     Active: active (running) since Fri 2025-06-20 17:38:41 IST; ...
     ...
Jun 20 17:38:41 practice-VirtualBox dnsmasq[1483]: started, version 2.90 cachesize 150
Jun 20 17:38:41 practice-VirtualBox dnsmasq[1483]: DNS service limited to local subnets
Jun 20 17:38:41 practice-VirtualBox dnsmasq[1483]: read /etc/hosts - 8 names
```

> **Note:** The warning about `resolvconf` can be safely ignored unless you're using advanced DNS forwarding or `systemd-resolved` integration.

---

# Verifying DNS Port Availability

Check if `dnsmasq` is listening on the standard DNS port (53):

```bash
sudo lsof -i :53
```

**Example Output:**

```
COMMAND  PID    USER     FD   TYPE  DEVICE SIZE/OFF NODE NAME
dnsmasq  1424   dnsmasq   4u  IPv4  ...    ...      UDP *:domain
dnsmasq  1424   dnsmasq   5u  IPv4  ...    ...      TCP *:domain (LISTEN)
dnsmasq  1424   dnsmasq   6u  IPv6  ...    ...      UDP *:domain
dnsmasq  1424   dnsmasq   7u  IPv6  ...    ...      TCP *:domain (LISTEN)
```

 This confirms that `dnsmasq` is correctly listening for both **IPv4 and IPv6** DNS requests over **UDP and TCP**.

---

# Checking for Conflicts (systemd-resolved)

To make sure no other process is conflicting with port 53:

```bash
sudo systemctl status systemd-resolved
```

**Result:**

```
● systemd-resolved.service - Network Name Resolution
     Loaded: loaded (...)
     Active: inactive (dead)
```

 `systemd-resolved` was **disabled**, so it did not interfere with `dnsmasq`.
If it were active, it might occupy port 53 and cause conflicts.

---
