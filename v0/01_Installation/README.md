# Step 01 - VirtualBox and Ubuntu Installation

## Objective
To set up a virtual machine using VirtualBox and install Ubuntu so we can later configure and run our private DNS server.


## Reference Video
Watch this step-by-step guide to install VirtualBox and Ubuntu:
[YouTube Video – Install VirtualBox and Ubuntu](https://youtu.be/nvdnQX9UkMY?si=ntb9taabC9k61p0j)

## What You Need
- Oracle VirtualBox (Installed on Windows or Linux host)
- Ubuntu ISO (e.g., `ubuntu-24.04.2-desktop-amd64.iso`)
- At least 2 GB RAM and 15–20 GB disk space allocated to the VM


## Installation Steps

1. **Download and Install VirtualBox**
2. **Download Ubuntu ISO**
3. **Create a new Virtual Machine in VirtualBox**
   - Select Type: Linux
   - Select Version: Ubuntu (64-bit)
   - Set Base Memory (RAM): 4 GB or more
   - Set Virtual Hard Disk Size: 25 GB minimum (Do not go beyond 50 GB)
4. **Attach Ubuntu ISO in storage settings**
5. **Start the VM and install Ubuntu**
   - Create username/password
   - You can use "Try Ubuntu" or "Install Ubuntu"


## Next Step - Install `dnsmasq` on Ubuntu

Once Ubuntu is installed and running, open a terminal in the VM and run:

```bash
sudo apt update
sudo apt install dnsmasq
```