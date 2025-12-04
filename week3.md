# Week 3 – Application Selection for Performance Testing

---

## Application Selection Matrix

To evaluate system performance under different workloads, I selected applications that represent **CPU-intensive**, **RAM-intensive**, **Disk I/O-intensive**, **Network-intensive**, and **Server workload** categories.

Each application was chosen because it is lightweight, easy to run on Ubuntu Server, and can generate measurable load.

### Application Selection Matrix

| Workload Type       | Application      | Justification |
|---------------------|------------------|---------------|
| **CPU-Intensive**   | `stress-ng`      | Can generate controlled CPU load, allows fine-tuned stress testing across multiple cores. |
| **RAM-Intensive**   | `stress-ng` (RAM mode) | Able to allocate large memory blocks to test memory pressure. |
| **Disk I/O-Intensive** | `fio`         | Industry-standard tool for benchmarking disk reads/writes and IOPS. |
| **Network-Intensive** | `iperf3`       | Creates measurable upload/download throughput between client and server. |
| **Server Application** | `nginx`       | Lightweight production-grade web server, useful for real-world request/performance testing. |

---

## Installation Documentation (All commands via SSH)

All applications will be installed **from the workstation using SSH**, not from VirtualBox console.

### Update package lists first:
```bash
ssh alex@192.168.56.20 "sudo apt update"

Once connected, the following commands install each tool:

  Update system first
sudo apt update && sudo apt upgrade -y

  Install CPU & RAM testing tool (stress-ng)
sudo apt install stress-ng -y

  Install Disk I/O benchmarking tool (fio)
sudo apt install fio -y

  Install network performance tool (iperf3)
sudo apt install iperf3 -y

  Install server application (nginx)
sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx


All these installations must be done via SSH and documented with screenshots in later weeks.

   Expected Resource Profiles

Below are the anticipated resource usage patterns for each application.
These predictions will be compared with real tests in Week 6.

  CPU-Intensive – stress-ng

Expected behaviour:

Very high CPU usage (90–100% per core)

Minimal RAM usage

No disk or network load

  RAM-Intensive – stress-ng (memory mode)

Expected behaviour:

Large RAM consumption depending on allocation

Swap activity if memory limit is exceeded

Low CPU usage

  Disk I/O-Intensive – fio

Expected behaviour:

High read/write activity on disk

Increase in IOPS and latency

CPU moderately used during I/O processing

   Network-Intensive – iperf3

Expected behaviour:

High network throughput (bandwidth test)

Measure upload/download speeds from workstation

Minimal CPU and disk load

  Server Application – nginx

Expected behaviour:

Low idle resource usage

Under load:

Moderate CPU usage

Slight RAM increase

Minimal disk activity

Fast response times for static content

   Monitoring Strategy

For each application, a specific measurement approach will be used. All commands will be executed remotely via SSH.

   CPU Testing (stress-ng)

Monitor with:

ssh alex@192.168.56.20 "top -b -n 1"
ssh alex@192.168.56.20 "vmstat 2 5"


Metrics collected:

CPU %

Load average

Context switching

Thermal throttling (if any)

4.2 RAM Testing (stress-ng memory)

Monitor with:

ssh alex@192.168.56.20 "free -h"
ssh alex@192.168.56.20 'vmstat 2 5'


Metrics collected:

RAM usage

Swap usage

Memory pressure

  Disk I/O Testing (fio)

Monitor with:

ssh alex@192.168.56.20 "iostat -x 2 5"
ssh alex@192.168.56.20 "vmstat 2 5"


Metrics collected:

IOPS

Read/write throughput

Disk latency

Disk utilisation %

   Network Testing (iperf3)

From workstation (as client):

iperf3 -c 192.168.56.20


From server (as server mode):

iperf3 -s


Metrics collected:

Bandwidth (Mbps)

Jitter

Packet loss

   Server Application Testing (nginx)

Monitor with:

ssh alex@192.168.56.20 "ss -tuna"
ssh alex@192.168.56.20 "top -b -n 1"


External test:

curl -I http://192.168.56.20


Metrics collected:

Response time

Active connections

Request throughput

  Week 3 Reflection

This week I selected the applications I will use to generate different workloads and built a clear plan on how to test them.
I now understand how each tool stresses a different part of the operating system and how I will monitor performance remotely.
This prepares me for Week 4 (initial configuration + security) and Week 6 (performance testing and charts).

  Week 3 Checklist
Requirement	Status	Evidence
Application Selection Matrix	✔️	Section 1
Installation Documentation	✔️	Section 2
Expected Resource Profiles	✔️	Section 3
Monitoring Strategy	✔️	Section 4
Reflection	✔️	Section 5
