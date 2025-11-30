# Week 3 – Application Selection for Performance Testing

---

## 1. Application Selection Matrix

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

## 2. Installation Documentation (All commands via SSH)

All applications will be installed **from the workstation using SSH**, not from VirtualBox console.

### Update package lists first:
```bash
ssh alex@192.168.56.20 "sudo apt update"

