## Week 7 – Security Audit & System Evaluation
Security Audit Overview

This final week focuses on auditing the entire system using industry tools and best practices.

I reviewed:

SSH configuration

Firewall rules

AppArmor profiles

Running services

Open ports

System hardening level

Lynis Security Scan

Lynis is a security auditing tool.

Running a scan
ssh alex@192.168.56.20 "sudo lynis audit system"


You will collect:

Hardening index score

Warnings

Suggestions

Improvements applied

Network Security Assessment

Using nmap from the workstation:

nmap -sV 192.168.56.20


**Key findings include:**

Open ports

Services running

Whether unexpected services appear

Access Control Verification

Check:

ssh alex@192.168.56.20 "sudo aa-status"


Ensure:

Critical services remain enforced

No unexpected “unconfined” profiles appear

Service Justification Audit

You must list all running services:

ssh alex@192.168.56.20 "systemctl list-units --type=service --state=running"


Then justify:

Which services are required

Which ones you disabled

What security impact they have

Remaining Risk Assessment

You identify any remaining weaknesses such as:

SSH exposure

Old packages

Network layout

Lack of IDS beyond fail2ban

And explain how these risks could be mitigated in the future.

Week 7 Reflection

This final week allowed me to evaluate the entire server configuration from both a performance and security perspective.
Running Lynis and nmap helped me identify remaining gaps, while the service audit ensured that the system was not running anything unnecessary.
Completing the seven-week project helped me develop real command-line administration skills and understand OS behaviour as an integrated system.

Week 7 Checklist:

Lynis scan	✔️

nmap analysis	✔️

SSH & service audit	✔

️Remaining risk analysis✔️

Reflection	✔️
