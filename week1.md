## System Architecture Diagram
<img width="751" height="668" alt="diagram" src="https://github.com/user-attachments/assets/9fa5787c-2c7b-4362-982b-272ac89fc540" />

## Distribution Selection Justification

For my server, I selected **Ubuntu Server 22.04 LTS (Long Term Support)**.

### Justification
Ubuntu Server provides a stable, secure, and well-documented environment ideal for headless administration and SSH management. It’s widely used in the cloud and enterprise environments, making it an excellent learning choice.

| Distribution | Advantages | Disadvantages | Suitability |
|---------------|-------------|----------------|--------------|
| **Ubuntu Server 22.04 LTS** | Excellent community support, 5-year security updates, modern package management (APT), easy SSH/firewall setup | Slightly higher resource usage than minimal distros | Best balance for learning and performance |
| **Debian 12** | Highly stable, minimal resource usage | Older software versions, slower update cycle | Good for production environments |
| **CentOS Stream 9** | Enterprise-grade, SELinux included | Complex setup, different package manager (dnf) | Best for Red Hat ecosystems |
| **Alpine Linux** | Extremely lightweight | Minimal default packages, steep learning curve | Ideal for containers, not general-purpose use |

**Decision Summary:**  
I chose **Ubuntu Server 22.04 LTS** because it offers the best mix of usability, documentation, and long-term support while remaining close to real-world server environments.

---

## Workstation Configuration Decision

For my workstation, I selected **Option B – Host Machine with SSH Client**.

### Justification
Using my host machine as the workstation provides a realistic and efficient workflow. It avoids unnecessary resource usage by running multiple VMs and mirrors how real administrators manage remote servers.

| Option | Description | Pros | Cons |
|--------|--------------|------|------|
| **A. Linux Desktop VM** | Separate VM for admin access | Isolation, Linux GUI | Consumes extra resources |
| **B. Host Machine with SSH Client** | Use host terminal for SSH | Simple, efficient, realistic | Less isolation |
| **C. Hybrid Setup** | Combination of host and VM tools | Flexible | More complex configuration |

**Chosen Option:** Host Machine (Option B)  
SSH will be used for all administrative tasks and file transfers.

---

## Network Configuration Documentation

The network is implemented through **VirtualBox Host-Only Networking**, enabling a private communication channel between the workstation and server.

### Planned VirtualBox Network Configuration

| Adapter | Type | Network | Purpose |
|----------|------|----------|----------|
| **Adapter 1** | Host-Only Adapter | `192.168.56.0/24` | SSH connection between workstation and server |
| **Adapter 2 (optional)** | NAT | Automatically assigned | Internet access for package updates |

### Planned IP Addressing

| System | Adapter | IP Address | Purpose |
|---------|----------|------------|----------|
| **Workstation (Host)** | Host-Only | `192.168.56.10` | SSH access to server |
| **Server (VM)** | Host-Only | `192.168.56.20` | Receives SSH connections |
| **VirtualBox Network** | Host-Only Network | `192.168.56.0/24` | Internal communication |

---

## CLI System Specification Documentation

The following commands will be used to document system information once both systems are deployed.  
Below are example outputs that show the type of data expected.

### Server CLI Commands

bash
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

## System Specification Evidence (CLI Screenshots)

Below is the required CLI output captured from my Ubuntu Server VM:

![System Specs Screenshot](./Oleksii-Personal/Pictures/Screenshots/week1-cli-output.png)
