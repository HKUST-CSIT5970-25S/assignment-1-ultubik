[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)

# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Ziyi QIN

### Student Id: 21135169

### Email: zqinas@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).
   
   > For CPU performance, I chose 7-Zip compression benchmark with decompression rating, which shows a value in MIPS calculated from the measured speed, and it can rate the values in single-thread or multi-thread mode close to real single or 2 CPU(s) frequency. Since the decompression rating values strongly depend on CPU integer oprations, thus it can value the CPU's capabilities and real-world performance since 7-zip is a daily application.
   > 
   > For memory performance, I chose ramspeed benchmark and I chose to carry out copy, add and scale actions on integer benchmark. It is because these types of actions on integer tests are rather fast and the results are steady. These operations are fundamental in scientific computing due to the large datasets frequently manipulated. The excution time, benchmark scores and metrics offer a comprehensive measurement of memory bandbidth and latency, which are important for optimizing performance in memory-intensive applications, scientific computing and so on.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?
   
    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.
   
   | Size        | CPU performance | Memory performance                                            |
   | ----------- | --------------- | ------------------------------------------------------------- |
   | `t2.micro`  | 3052 MIPS       | Add: 10384.56 MB/s; Copy: 10756.52 MB/s; Scale: 10010.96 MB/s |
   | `t2.medium` | 5948 MIPS       | Add: 19331.67 MB/s; Copy: 19665.22 MB/s; Scale: 18404.47 MB/s |
   | `c5d.large` | 4899 MIPS       | Add: 13597.66 MB/s; Copy: 13631.28 MB/s; Scale: 13640.32 MB/s |
   
   > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.
   
   | Type                      | TCP b/w (Mbps) | RTT (ms) |
   | ------------------------- | -------------- | -------- |
   | `t3.medium` - `t3.medium` | 4249.6         | 0.293    |
   | `m5.large` - `m5.large`   | 5089.28        | 0134     |
   | `c5n.large` - `c5n.large` | 4628.28        | 0.157    |
   | `t3.medium` - `c5n.large` | 1305.6         | 0.694    |
   | `m5.large` - `c5n.large`  | 2570.24        | 0.157    |
   | `m5.large` - `t3.medium`  | 2631.68        | 0.623    |
   
   > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.
   
   | Connection                | TCP b/w (Mbps) | RTT (ms) |
   | ------------------------- | -------------- | -------- |
   | N. Virginia - Oregon      | 32.3           | 63.149   |
   | N. Virginia - N. Virginia | 3952.64        | 0.094    |
   | Oregon - Oregon           | 5089.28        | 0.197    |
   
   > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
