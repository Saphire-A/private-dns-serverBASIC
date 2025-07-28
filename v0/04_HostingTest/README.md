### goal
```
Host a sample website locally and access it using your custom domain (e.g., example.test)?
Connect the private DNS server to a real web service (Apache, Nginx)?
Test resolution beyond ping and dig — e.g., in a browser? 
```
install apache2:
commands:
1) sudo apt update
2) sudo apt install apache2 --> installs the appache2 server
3) systemctl status apache2 --> check if the server is running
You should see Active: active (running). If it isn’t running:
sudo systemctl start apache2

🌐 Next Step : Test in Browser
Open your browser in the VM and visit:

arduino
Copy code
http://localhost
If it shows the Apache2 Ubuntu Default Page — you’re good! 🎉

