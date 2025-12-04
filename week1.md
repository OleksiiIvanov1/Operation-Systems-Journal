## Week 1 – System Setup and Initial Planning
System Architecture Diagram

<img width="751" height="668" alt="diagram" src="https://github.com/user-attachments/assets/9fa5787c-2c7b-4362-982b-272ac89fc540" />

This is the basic layout I planned for the coursework: a headless Ubuntu Server VM running in VirtualBox, and my host computer acting as the workstation. All administration will be done through SSH, not the VirtualBox console.

**Choosing the Server Distribution**

For the server OS, I went with Ubuntu Server 22.04 LTS.
My goal was to use something stable, well-documented, and close to what’s used in real cloud environments. Ubuntu Server ticked all those boxes.

Here’s the comparison I made while deciding:

Distribution	Advantages	Disadvantages	Suitability
Ubuntu Server 22.04 LTS	Strong community support, long-term updates, easy to configure SSH and firewall	A bit heavier than minimal distros	Great for learning + real-world use
Debian 12	Very stable, lightweight	Older packages	Better for production machines
CentOS Stream 9	SELinux built-in, enterprise-focused	Uses dnf, different workflow	Good for Red Hat users
Alpine Linux	Super lightweight	Harder for beginners, minimal tools	Best for containers

Why I chose Ubuntu Server 22.04:
It’s reliable, familiar, and widely supported. For this coursework I need to configure a lot of different tools, and Ubuntu makes that much smoother.

**Workstation Setup Decision**

For the workstation, I decided to use my host machine with an SSH client instead of a second VM.

Why:
Running two VMs at the same time slows everything down. Using my host machine feels more realistic because in real life admins normally SSH into servers from their own computer anyway.

Comparison I made:

Option	Pros	Cons
Linux Desktop VM	Clean separation, GUI available	Uses more system resources
Host Machine (SSH client)	Simple, fast, realistic workflow	Less isolated than having 2 VMs
Hybrid	Very flexible	More complicated setup

So I went with Option B (Host Machine + SSH).

**Network Configuration Plan**

The server and workstation communicate through VirtualBox Host-Only Networking.
This keeps everything isolated from the external network, which is required for the module.

VirtualBox Adapter Setup
Adapter	Type	Network	Purpose
Adapter 1	Host-Only	192.168.56.0/24	Main SSH connection
Adapter 2 (optional)	NAT	Internet access for updates	
Planned IP Addresses
System	IP Address	Purpose
Workstation (Host)	192.168.56.10	SSH into server
Server VM	192.168.56.20	Receives SSH connections
Host-Only Network	192.168.56.0/24	Private internal network
Server System Information (CLI Output)

After getting the VM running, I used SSH to gather the system information required for Week 1.

$ uname -a
Linux server 5.15.0-92-generic #102-Ubuntu SMP x86_64 GNU/Linux

$ free -h
              total        used        free      shared  buff/cache   available
Mem:           2048Mi       120Mi      1600Mi        10Mi       328Mi      1820Mi

$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        20G  1.5G   18G   8% /

$ ip addr
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500
    inet 192.168.56.20/24 brd 192.168.56.255 scope global enp0s3

$ lsb_release -a
Distributor ID: Ubuntu
Description:    Ubuntu 22.04.3 LTS
Release:        22.04
Codename:       jammy

![Week 1 CLI Output](/images/week1-cli-output.png)

**Reflection on Week 1**

Most of this week was about planning the environment, getting VirtualBox working properly, and checking that I could actually SSH into the server.
At first VirtualBox refused to start any VMs because virtualisation was turned off in BIOS, so I had to fix that.
After that, networking took a bit of trial and error because the Host-Only adapter didn’t have an IP at first, but once I updated the settings it worked and I could gather system information through SSH.

Overall, Week 1 set the foundation for everything else. Next week I’ll focus on the security and performance testing plan.

**Week 1 Checklist:**

System Architecture Diagram	- completed

Distribution Selection	- completed

Workstation Choice	- completed

Network Configuration	- completed

CLI Evidence	- completed

Reflection	- completed
