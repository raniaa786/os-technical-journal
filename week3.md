This week focused on choosing the applications and tools that I will use to test the performance of my Ubuntu Server. The aim was to pick software that allows me to simulate different workload types (CPU, RAM, I/O, and network) so that I can evaluate how the system behaves under stress.

Even though I am not installing anything yet, documenting the installation commands and understanding what each tool does will help me prepare for the testing stages in later weeks.

1. Applications I Selected and Why
1. Apache Web Server (Network-intensive)

I chose Apache because:

it is one of the most commonly used web servers

it is easy to configure

it allows me to generate real network and CPU load

there is a lot of documentation available

Apache provides a realistic service to test when I perform network benchmarking in Week 6.

2. stress-ng (CPU, memory, and I/O workloads)

I selected stress-ng because it allows me to create synthetic workloads that target CPU, RAM, and storage. This is useful for understanding how the server behaves under different types of load.

3. apache2-utils (ab benchmarking tool)

The ab tool sends a large number of HTTP requests to Apache to measure:

response time

throughput

server capacity

This makes it ideal for testing Apache’s performance during benchmarking.

4. htop (Monitoring tool)

I am including htop because it gives a clear, real-time view of CPU usage, memory usage, load averages, and processes. It helps me observe what the system is doing during stress tests.

2. Installation Commands (Documentation Only)

These are the commands I will use later via SSH to install the applications:

sudo apt update
sudo apt install apache2
sudo apt install apache2-utils
sudo apt install stress-ng
sudo apt install htop

3. Expected Resource Usage

Apache:
Uses network, RAM, and CPU resources depending on how many requests it handles.

ab tool:
CPU-intensive while generating HTTP requests.

stress-ng:
Can fully saturate CPU cores, fill memory, or create I/O load depending on the test.

htop:
Very lightweight; used mainly for observing performance changes.

4. Monitoring Strategy

To measure system performance, I plan to use:

htop for real-time monitoring

top as an alternative

free -h to track memory use

df -h to track disk space

ab for benchmarking Apache

Apache log files for request data


This will allow me to compare the server’s behaviour under idle conditions and under different types of load.


This week was focused on selecting and planning the tools I will use later to test and benchmark my server. The applications I chose give me a variety of workloads to analyse without making the system overly complicated.
