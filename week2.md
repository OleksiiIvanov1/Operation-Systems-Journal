# Week 2 – Security Planning and Testing Methodology

---

## 1. Performance Testing Plan

### 1.1 Purpose of Performance Testing
The purpose of this performance testing plan is to establish a clear and repeatable methodology for evaluating the performance of my Ubuntu Server 22.04 LTS system.  
This testing will later be used in Week 6 for data visualisation, bottleneck identification, and optimisation.

The goals of the performance testing plan are:

- Measure system behaviour under different workloads  
- Collect CPU, memory, disk I/O, and network performance data  
- Ensure all monitoring is done **remotely over SSH**  
- Maintain consistency across all performance tests  
- Prepare for advanced analysis and optimisation later in the project  

---

### 1.2 Remote Monitoring Methodology

All performance testing will be executed **from my workstation**, never from the VirtualBox console.  
Only SSH will be used to interact with the server.

Remote access command:

bash
ssh alex@192.168.56.20

Monitoring Tools Used During Testing

These tools will be executed remotely through SSH:

Tool	Purpose
top / htop	Live CPU and memory usage
vmstat	System-wide performance snapshot
iostat	Detailed disk I/O performance
free -h	Memory usage
df -h	Disk usage summary
ss -tuna	Network connections overview
ping	Latency measurement
journalctl	Logs for warnings and errors

Example Remote Monitoring Commands

All commands are executed from the workstation:

ssh alex@192.168.56.20 "top -b -n 1"
ssh alex@192.168.56.20 "vmstat 2 5"
ssh alex@192.168.56.20 "iostat -x 2 5"
ssh alex@192.168.56.20 "free -h"
ssh alex@192.168.56.20 "df -h"
ssh alex@192.168.56.20 "ss -tuna"

2. Security Configuration Checklist

This checklist defines all the security measures I will implement in later weeks (4–5).
For Week 2, this serves as planning and documentation.

SSH Hardening

Disable password authentication

Enable key-based authentication

Change default SSH port (optional, explained later)

Limit login to specific users

Restrict SSH to only the workstation IP

Firewall Configuration (UFW)

Enable UFW

Allow SSH only from the workstation

Deny all other inbound traffic

Allow required ports for performance tests (if needed)

Mandatory Access Control (AppArmor or SELinux)

Ensure AppArmor profiles are loaded (Ubuntu default)

Audit logs for denied operations

Apply strict profiles for selected services

Automatic Updates

Enable unattended-upgrades

Apply automatic security patches

Log update activity for verification

User Privilege Management

Create a non-root admin user

Configure sudo securely

Restrict file permissions

Disable root SSH login

Network Security

Disable unused network services

Verify open ports with ss -tuna and nmap

Implement fail2ban (later in Week 5)

Use host-only network isolation in VirtualBox

3. Threat Model

This threat model identifies realistic threats to my server system and provides mitigation strategies for each one.

Threat 1: Brute-Force SSH Attacks

Risk: Attackers repeatedly try random passwords to gain access.
Impact: Full system compromise if successful.

Mitigation:

Disable password authentication

Use key-based authentication

Restrict SSH to workstation IP only

Enable fail2ban later in Week 5

Threat 2: Unpatched Vulnerabilities

Risk: Outdated packages or kernel vulnerabilities can be exploited.
Impact: Remote code execution, privilege escalation, system compromise.

Mitigation:

Enable automatic security updates

Regularly check update logs

Use LTS distribution (Ubuntu 22.04)

Perform weekly manual update checks

Threat 3: Unauthorized Network Access

Risk: Attackers scanning the local network could reach the VM.
Impact: Unauthorized access or exploitation.

Mitigation:

Use VirtualBox Host-Only network isolation

Enable a strict firewall (UFW)

Disable unused services and ports

Monitor open ports using ss, netstat, and nmap

Week 2 Reflection

This week I created a full security planning structure and a monitoring methodology that will be used in later phases.
I now understand which tools I will rely on for performance testing and how to secure the server before implementing any services.
My threat model helped me clearly define risks and plan realistic countermeasures.

Next week I will move on to application selection and installation for the performance testing.

Week 2 Deliverables Checklist
Requirement	Status	Evidence
Performance Testing Plan	✔️	Section 1
Security Configuration Checklist	✔️	Section 2
Threat Model	✔️	Section 3
Reflection	✔️	Section above
