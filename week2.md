# Week 2 – Security Planning and Testing Methodology

## 1. Performance Testing Plan

### 1.1 Goals

The goal of my performance testing is to:

- Measure how my Ubuntu Server 22.04 LTS behaves under different workloads (CPU, RAM, disk, and network).
- Collect **quantitative data** (CPU %, memory usage, I/O, latency) remotely via SSH from my workstation.
- Reuse the same methodology later in Week 6 for full performance evaluation and visualisations.

All monitoring and testing will be done **remotely over SSH** from my host machine (workstation) to the VirtualBox server VM. No local console will be used on the server.

---

### 1.2 Remote Monitoring Methodology

**Access method:**  
- Use SSH from the host (workstation) to the server:  
  `ssh alex@192.168.56.20` (example IP from Week 1)

**Monitoring tools on the server (run via SSH):**

- `top` / `htop` – live process and CPU/memory overview.
- `vmstat` – overall system performance (CPU, memory, swap, I/O).
- `iostat` (from `sysstat` package) – disk I/O statistics.
- `free -h` – memory usage summary.
- `df -h` – disk space usage.
- `ss -tuna` – network connections and listening ports.
- `ping` – network latency testing.
- `journalctl` – system logs for error / warning correlation.

**Example remote commands from workstation:**

```bash
ssh alex@192.168.56.20 "top -b -n 1"
ssh alex@192.168.56.20 "vmstat 2 5"
ssh alex@192.168.56.20 "iostat -x 2 5"
ssh alex@192.168.56.20 "free -h"
ssh alex@192.168.56.20 "df -h"
ssh alex@192.168.56.20 "ss -tuna"

