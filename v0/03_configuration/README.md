# Step 03 - DNSMasq Configuration

## Objective
To configure `dnsmasq` to resolve a custom domain name (like `example.test`) to a local IP address (`192.168.0.100`) using a private DNS setup.

---

## Files Modified

`/etc/dnsmasq.conf`  
> This is the main configuration file for `dnsmasq`.  
> **Do NOT rename or move this file.**

---

## Step-by-Step Configuration

1. Edit the dnsmasq config file

Run this command in terminal:
```bash
sudo nano /etc/dnsmasq.conf


2. Add the custom DNS entry
Scroll to the bottom of the file and add:

address=/example.test/192.168.0.100
Do NOT use #address=... — the # symbol will comment out the line.
We switched from .local to .test to avoid conflicts with mDNS (Multicast DNS).

To save and exit Nano:
Press Ctrl + O, then Enter to save
Press Ctrl + X to exit

3. Restart the dnsmasq service
sudo systemctl restart dnsmasq
Be careful typing systemctl — don’t confuse lowercase L with the number 1.

4. Test DNS Resolution
Option A: Using dig
dig example.test @127.0.0.1
Expected Output:

;; ANSWER SECTION:
example.test.     0     IN     A     192.168.0.100
If dig is not installed:

sudo apt install dnsutils
Option B: Using ping

ping example.test
If successful, this should resolve to 192.168.0.100.

Warnings & Tips
.local domains are reserved for Multicast DNS (mDNS).
So:

dig example.local may work (because it directly queries your DNS)
But ping example.local may fail, because the system tries mDNS first.
Use .test, .home, or .lab for private/local domains.
dig is better than ping for DNS testing because it talks directly to the DNS server, not the whole system resolver.

Final Confirmation
Run:
ping example.test
If you see:
PING example.test (192.168.0.100) ...
Congratulations! Your private DNS with dnsmasq is working properly!

