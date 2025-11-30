# Week 2 – Security Planning and Testing Methodology

---

## 1. Performance Testing Plan

### 1.1 Purpose of Performance Testing
The purpose of this performance testing plan is to create a consistent and repeatable method for evaluating the performance of my Ubuntu Server 22.04 LTS system.

This performance testing will later support Week 6, where I will produce:
- Performance graphs  
- Bottleneck identification  
- Optimisation testing  
- Quantitative analysis  

The testing goals are:
- Measure CPU, RAM, disk I/O, and network behaviour  
- Collect accurate data remotely  
- Ensure repeatable test methodology  
- Prepare the foundation for deeper analysis later  

---

### 1.2 Remote Monitoring Methodology

All performance testing will be executed **from my workstation via SSH**.

#### Remote SSH Access
```bash
ssh alex@192.168.56.20
Monitoring Tools Used
Tool	Purpose
top / htop	Live CPU & RAM usage
vmstat	System-wide stats (CPU, memory, I/O)
iostat	Disk I/O performance
free -h	Memory usage overview
df -h	Disk space usage
ss -tuna	Network connections & listening ports
ping	Latency and packet loss
journalctl	System logs for warnings & errors

Example Remote Commands
These are executed from the workstation, not inside VirtualBox:

bash
Copy code
ssh alex@192.168.56.20 "top -b -n 1"
ssh alex@192.168.56.20 "vmstat 2 5"
ssh alex@192.168.56.20 "iostat -x 2 5"
ssh alex@192.168.56.20 "free -h"
ssh alex@192.168.56.20 "df -h"
ssh alex@192.168.56.20 "ss -tuna"
2. Security Configuration Checklist
This checklist outlines the security measures I will implement in Weeks 4 and 5.
For Week 2, this document serves as planning.

✔ SSH Hardening
Disable password authentication

Enable key-based authentication

Restrict SSH to specific users

Allow SSH only from the workstation IP

Disable root login

(Optional) Change default SSH port

✔ Firewall Configuration (UFW)
Enable UFW

Allow SSH only from workstation

Deny all other incoming traffic

Allow ports only when required for testing

✔ Mandatory Access Control (AppArmor / SELinux)
Ensure AppArmor is enabled

Check loaded profiles

Monitor denied activity in logs

Apply strict profiles to selected services

✔ Automatic Security Updates
Enable unattended-upgrades

Apply security patches automatically

Log update actions for verification

✔ User Privilege Management
Create a non-root admin user

Configure secure sudo usage

Restrict file permissions

Disable direct root access

✔ Network Security
Disable unnecessary network services

Verify open ports with ss and nmap

Implement fail2ban (Week 5)

Use Host-Only network isolation

3. Threat Model
Threat 1: Brute-Force SSH Attacks
Risk: Attackers attempt password guessing.
Impact: Full system compromise.

Mitigation:

Disable password authentication

Enforce key-based authentication

Restrict SSH to workstation IP

Enable fail2ban (Week 5)

Threat 2: Unpatched Vulnerabilities
Risk: Exploit outdated packages or kernel vulnerabilities.
Impact: Remote code execution, privilege escalation.

Mitigation:

Enable automatic security updates

Weekly manual update checks

Use Ubuntu LTS for long-term stability

Threat 3: Unauthorized Network Access
Risk: Attackers scan VirtualBox network and target the VM.
Impact: Unauthorized service access or exploitation.

Mitigation:

Restrictive firewall (UFW)

Host-only isolation

Disable unused services

Monitor ports using ss and nmap

4. Week 2 Reflection
This week I created a complete security planning structure and performance testing methodology.
I learned which tools will be used to monitor system behaviour and how to securely prepare the server before installing any applications.

My threat model helped me define realistic risks and choose proper mitigation strategies.

Next week, I will select applications for load testing and prepare installation documentation.

5. Week 2 Deliverables Checklist
Requirement	Status	Evidence
Performance Testing Plan	✔️	Section 1
Security Configuration Checklist	✔️	Section 2
Threat Model	✔️	Section 3
Reflection	✔️	Section 4
