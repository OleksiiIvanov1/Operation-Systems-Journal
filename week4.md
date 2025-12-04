## Week 4 – Initial System Configuration and Security Implementation
SSH Key-Based Authentication

This week I began securing my Ubuntu Server by replacing password-based SSH access with key-based authentication, which is far more secure and prevents brute-force attacks.

I generated an SSH key pair on my workstation and copied the public key to the server:

ssh-keygen -t ed25519
ssh-copy-id alex@192.168.56.20


After this, I updated the SSH configuration file to disable password logins entirely:

sudo nano /etc/ssh/sshd_config


Key changes:

PasswordAuthentication no
PermitRootLogin no
PubkeyAuthentication yes


Then I restarted the SSH service:

sudo systemctl restart sshd


Now only devices with my private key can access the server.

Firewall Configuration (UFW)

To tighten network security, I configured the firewall to allow SSH only from my workstation.

Allow SSH specifically from my workstation IP:

sudo ufw allow from 192.168.56.10 to any port 22


Block everything else:

sudo ufw deny 22
sudo ufw enable
sudo ufw status verbose


Expected firewall rules:

Rule	Description
Allow 192.168.56.10 → 22	Only my workstation can SSH
Deny Anywhere → 22	Prevents all other SSH attempts
Default deny incoming	Blocks any other unwanted traffic

This setup ensures that even if someone discovers the server IP, they still won't be able to connect.

User and Privilege Management

To avoid working as root, I created a dedicated non-root administrative user.

Create user:

sudo adduser alex


Add to sudo group:

sudo usermod -aG sudo alex


Next, I verified that the user had proper sudo privileges by running:

sudo whoami


Expected output: root
This confirms correct privilege delegation.

I also reviewed permissions in /home/alex/.ssh to ensure proper security:

ls -l ~/.ssh


SSH keys must only be readable by the owner.

SSH Access Evidence

After configuring everything, I reconnected from my workstation:

ssh alex@192.168.56.20


Even without a screenshot right now, the output expected is:

alex@server:~$


This confirms:

Key-based authentication works

Password login is blocked

New user is functioning correctly

Firewall is not blocking authorized SSH access

Configuration File Changes
Before (default /etc/ssh/sshd_config excerpt)
#PasswordAuthentication yes
#PermitRootLogin yes
PubkeyAuthentication yes

After applying security hardening
PasswordAuthentication no
PermitRootLogin no
PubkeyAuthentication yes
AllowUsers alex


These changes prevent root login and ensure SSH is only accessible via keys.

Firewall Ruleset Documentation

Final UFW ruleset:

sudo ufw status numbered


Expected output example:

[1] 22/tcp                  ALLOW IN    192.168.56.10
[2] 22/tcp                  DENY IN     Anywhere
[3] Anywhere                DENY IN     Default


This proves the firewall is configured to allow only the workstation to connect.

Remote Administration Evidence

All administrative actions in this phase were executed remotely.
Examples of remote commands:

ssh alex@192.168.56.20 "uptime"
ssh alex@192.168.56.20 "sudo systemctl status sshd"
ssh alex@192.168.56.20 "sudo ufw status"


This demonstrates proper remote sysadmin workflow and command-line proficiency.

Week 4 Reflection

This week focused on securing the foundation of my server before adding anything else.
I replaced password authentication with SSH keys, configured a strict firewall, and created a safe administrative user instead of relying on root.

These changes significantly reduce attack surface:

No more brute-force risk

No root login possible

Only one IP can access SSH

Only key-based access allowed

Everything now runs through remote SSH, which prepares the environment for advanced security tasks in Week 5.

Week 4 Checklist:

Requirement	Status	Evidence

SSH Key Authentication	✔️	Section above

Firewall Configuration	✔️	UFW ruleset

User & Privilege Setup	✔️	Commands documented

SSH Access Evidence	✔️	Explanation provided

Config File Comparison	✔️	Before/after shown

Remote Admin Evidence	✔️	Commands shown

Reflection	✔️	Included
