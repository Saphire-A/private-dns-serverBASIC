## Step 03 - DNSMasq Configuration

# Objective
Configure dnsmasq to resolve a custom domain name (like example.test) to a local IP address (192.168.0.100) as part of your private DNS setup.

# Files Modified
/etc/dnsmasq.conf

Main configuration file for dnsmasq.
⚠️ Do NOT rename or move this file.

# Step-by-Step Configuration
1. Edit the dnsmasq config file
bash
sudo nano /etc/dnsmasq.conf

2. Add the custom DNS entry
Scroll to the bottom of the file and add:

bash
address=/example.test/192.168.0.100

🔸 Do NOT use #address=... — the # symbol comments the line.
🔸 Using .test instead of .local avoids Multicast DNS (mDNS) conflicts.

To save and exit Nano:

Press Ctrl + O, then Enter (Save)

Press Ctrl + X (Exit)

3. Restart the dnsmasq service
```bash
sudo systemctl restart dnsmasq
```

⚠️ Be careful typing systemctl — don’t confuse lowercase L with the number 1.

4. Test DNS Resolution

4.1 Using dig
```bash
dig example.test @127.0.0.1
```

Expected Output:

;; ANSWER SECTION:
example.test.     0     IN     A     192.168.0.100
If dig is not installed:

```bash
sudo apt install dnsutils
```


4.2 Using ping
```bash
ping example.test
```
If it resolves to 192.168.0.100, your configuration is working!

⚠️ Warnings & Tips
.local domains are reserved for Multicast DNS (mDNS).

Example:

dig example.local may work.
ping example.local might fail due to mDNS override.
Recommended domains: .test, .home, .lab.
dig is better than ping for DNS testing — it queries the DNS server directly.

Final Confirmation
Run:
```bash
ping example.test
```
If you see:

```bash
PING example.test (192.168.0.100) ...
```
🎉 Congratulations! Your private DNS with dnsmasq is working perfectly.