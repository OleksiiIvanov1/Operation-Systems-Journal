# Week 2 – Security Planning and Testing Methodology

---

## 1. Performance Testing Plan

### 1.1 Purpose of Performance Testing
The purpose of this performance testing plan is to define how I will measure and analyse the performance of my Ubuntu Server 22.04 LTS during different workloads later in the coursework.  
This includes:

- Measuring CPU, memory, disk I/O, and network usage
- Running all tests **remotely over SSH**
- Collecting consistent and repeatable performance data
- Preparing the methodology required for Week 6 performance evaluation

All monitoring will be done remotely from the workstation (host machine), never from the VirtualBox console.

---

### 1.2 Remote Access Method
All tests will be executed remotely using SSH.

Example connection command:

```bash
ssh alex@192.168.56.20
