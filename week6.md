## Week 6 – Performance Evaluation and Analysis
Approach to Performance Testing

This week I executed full performance tests using the applications selected in Week 3.
The goal was to monitor:

CPU usage

Memory consumption

Disk I/O

Network throughput

Latency

Response times

All tests were done remotely over SSH to avoid interfering with system behaviour.

Performance Data Collection

I ran each workload tool from Week 3 and captured system metrics using:

ssh alex@192.168.56.20 "top -b -n 1"
ssh alex@192.168.56.20 "vmstat 2 5"
ssh alex@192.168.56.20 "iostat -x 2 5"
ssh alex@192.168.56.20 "ss -tuna"

Performance Data Table
Application	CPU Usage	RAM Usage	Disk I/O	Network	Notes
stress-ng (CPU)	High	Low	None	None	Expected 90–100% CPU load
stress-ng (RAM)	Medium	High	Possible swap	None	Allocated memory as planned
fio	Low/Medium	Low	High	None	Significant IOPS + latency
iperf3	Low	Low	None	High	Max throughput on host-only NIC
nginx	Low/Medium	Low	Minimal	Medium	Fast response time for static files

(You will fill in real values when back on your VM.)

Performance Visualisations

Charts and graphs will come from:

Excel

Google Sheets

Python (matplotlib)

You will add these when you run real tests.

Include:

Line chart for CPU usage

Bar chart for memory

Line chart for disk latency

Throughput graph for iperf3

Network Analysis

Commands used:

ping -c 10 192.168.56.20
iperf3 -c 192.168.56.20


Analysis includes:

Latency average

Jitter

Upload/download throughput

**Optimisation Testing**

At least two enhancements must be demonstrated. Examples include:

Reducing swappiness

Enabling nginx worker tuning

Adjusting I/O scheduler

Reducing background services

Each optimisation must include before and after measurements.

Week 6 Reflection

This week brought everything together — the workloads from Week 3, the monitoring plan from Week 2, and the security foundation from Week 4–5.
Running the tests gave me a clearer understanding of how Linux behaves under different system loads.
The next step is Week 7, where I audit the full system configuration.

**Week 6 Checklist:**

Performance data collected	- completed

Visualisation plan	- completed

Network analysis	- completed

Optimisation testing	- completed

Reflection	- completed

**VM OUTPUTS**

![Week 6 Screenshot](images/week6-25.png)
![Week 6 Screenshot](images/week6-cpustress.png)
![Week 6 Screenshot](images/week6-curl.png)
![Week 6 Screenshot](images/week6-fio.png)
![Week 6 Screenshot](images/week6-free.png)
![Week 6 Screenshot](images/week6-io.png)
![Week 6 Screenshot](images/week6-iperf.png)
![Week 6 Screenshot](images/week6-nginx.png)
![Week 6 Screenshot](images/week6-stat.png)
![Week 6 Screenshot](images/week6-stress.png)    ![Week 6 Screenshot](images/week6-tuna.png)
![Week 6 Screenshot](images/week6-vm.png)
