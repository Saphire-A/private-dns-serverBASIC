# Step 04 – Host a Local Website & Resolve with Custom Domain

## Objective

- Host a sample website locally using Apache
- Access it using a custom domain like `example.test` via your private DNS (dnsmasq)
- Test the domain resolution inside a browser — beyond `ping` and `dig`


## Install Apache2 (Web Server)

Apache2 will serve your local web pages.

Run the following commands:

```bash
sudo apt update
sudo apt install apache2
```
Check the Apache service status:

```bash
systemctl status apache2
```
✅ Look for: Active: active (running)

If it's not running, start it manually:

```bash
sudo systemctl start apache2
```
Test in Browser
Open a browser inside your VM and visit:

http://localhost
You should see the Apache2 Ubuntu Default Page.
This confirms that Apache is installed and serving web content locally. 🎉

Test Custom Domain (Private DNS + Web Server)
Now try visiting:
http://example.test
If your dnsmasq is correctly configured and Apache is running:

The browser should resolve example.test to 192.168.0.100

You’ll again see the Apache default page
This means your private DNS and web server are integrated successfully.

Summary
Component	Status Check
dnsmasq	ping example.test or dig example.test
apache2	systemctl status apache2 and http://localhost
Browser Test	http://example.test should show default page

Optional
To host your own page, replace the default HTML file:

```bash
sudo nano /var/www/html/index.html
```
Type your custom HTML, save, and refresh the browser.

🎉 Done! You've now successfully configured a private DNS server and hosted a local website mapped to a custom domain name.