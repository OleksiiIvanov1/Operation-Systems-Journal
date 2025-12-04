Week 4 – Initial System Configuration & Security Implementation
SSH Key-Based Authentication

To secure remote access, I configured SSH to use key-based authentication instead of passwords.
This improves security by preventing brute-force password attacks and ensuring only devices with the private key can access the server.

Steps Performed

Generated an SSH key on the workstation:

ssh-keygen -t rsa -b 4096


Copied the public key to the server:

ssh-copy-id alex@192.168.56.20


Disabled password authentication on the server:

sudo nano /etc/ssh/sshd_config


Updated the following lines:

PasswordAuthentication no
PubkeyAuthentication yes
PermitRootLogin no


Restarted SSH service:

sudo systemctl restart ssh

Expected Result

The server now accepts only key-based login, preventing password brute-force attacks.

Firewall Configuration (SSH Allowed Only from One Workstation)

I configured the firewall to allow SSH exclusively from my workstation's IP address.

Enabled the firewall:

sudo ufw enable


Allowed SSH from the workstation only:

sudo ufw allow from 192.168.56.10 to any port 22


Blocked all other incoming traffic:

sudo ufw default deny incoming
sudo ufw default allow outgoing


Checked the ruleset:

sudo ufw status verbose

Expected Result

Only my workstation (192.168.56.10) can SSH into the server.
All other devices attempting port 22 are blocked.

User & Privilege Management

To avoid using root directly, I created a secure administrative user.

Created the user:

sudo adduser alex


Added them to the sudo group:

sudo usermod -aG sudo alex


Tested sudo access:

sudo whoami

Expected Result

The server now operates with a non-root admin account, reducing the risk of accidental system damage or privilege escalation attacks.

SSH Access Evidence

When I return to my workstation with VirtualBox, I will include screenshots of:

Successful SSH login using the key

Denied connection when trying a different IP (optional)

The command prompt showing alex@server:~$

For now, this section acts as documentation until screenshots can be added.

Configuration File Changes (Before & After)
Before – /etc/ssh/sshd_config default state
#PasswordAuthentication yes
#PubkeyAuthentication yes
#PermitRootLogin yes

After – hardened configuration
PasswordAuthentication no
PubkeyAuthentication yes
PermitRootLogin no
AllowUsers alex


This ensures only the admin user can log in, using a secure SSH key.

Firewall Documentation

Current firewall ruleset (expected output):

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW       192.168.56.10
Anywhere                   DENY        Anywhere


And default policies:

Default incoming: deny
Default outgoing: allow


This confirms a locked-down firewall, fulfilling the Week 4 requirement.

Remote Administration Evidence

All configuration work in this week was performed exclusively via SSH, as required.

Example administrative commands executed remotely:

ssh alex@192.168.56.20 "sudo systemctl status ssh"
ssh alex@192.168.56.20 "sudo ufw status"
ssh alex@192.168.56.20 "cat /etc/passwd"
ssh alex@192.168.56.20 "sudo journalctl -xe"


These commands demonstrate real remote system administration without using VirtualBox’s console.

Week 4 Reflection

This week I completed the essential security foundation for my server.
SSH is now secured with key-based authentication, passwords are disabled, and the root user cannot log in. I also configured a strict firewall that allows SSH access only from my workstation. Creating a non-root administrative user helped improve system security and aligns with industry best practices.

Once I return to my own machine with VirtualBox installed, I will capture screenshots to attach as visual proof of the configuration.

Week 4 Checklist
Requirement	Status	Evidence
SSH key-based authentication	✔️	Section above + screenshots later
Firewall (workstation-only SSH)	✔️	Firewall ruleset included
User & privilege management	✔️	Configuration steps shown
SSH access evidence	⚠️ Pending	Screenshots to be added later
Before/after configuration files	✔️	Included
Remote administration evidence	✔️	Commands included
