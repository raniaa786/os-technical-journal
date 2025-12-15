In this phase, I tested how the server behaves under load and monitored the impact on system resources. This helps identify potential performance bottlenecks and shows how the system reacts during high usage scenarios.

To test CPU performance, I used the stress-ng tool to generate artificial load on the processor:

stress-ng --cpu 2 --timeout 60s


This command applied load to two CPU cores for 60 seconds. During the test, the system produced debug and error messages, which is expected when running stress tests inside a virtual machine. Despite this, CPU usage increased significantly, confirming that the workload was being applied.

I then tested memory usage using:

stress-ng --vm 1 --vm-bytes 1G --timeout 60s


This command allocated 1GB of virtual memory to simulate high memory usage. The test showed increased memory consumption, demonstrating how the system handles memory pressure.

While the stress tests were running, I monitored the system in real time using htop. This allowed me to observe CPU usage spikes, running processes, and overall system load. The CPU bars clearly showed increased activity, and system responsiveness was slightly reduced during peak load, which is expected behaviour.

To further analyse system performance, I checked memory and load statistics using:

free -h
uptime


These commands confirmed the amount of memory in use and showed the system load averages during and after the stress tests. The server remained stable throughout the testing process and recovered quickly once the stress tests completed.

Overall, this phase demonstrated that the server can handle temporary high-load conditions while remaining operational. Monitoring tools such as htop, free, and uptime are essential for understanding system performance and diagnosing issues in real-world environments.

<img width="1216" height="694" alt="image" src="https://github.com/user-attachments/assets/c5199825-57ac-4fb7-9f06-2b5ef1cc5fa5" />

<img width="1218" height="723" alt="image" src="https://github.com/user-attachments/assets/3af244e7-eb83-4a2f-b1ca-0c9d0fbd122c" />

<img width="1216" height="718" alt="image" src="https://github.com/user-attachments/assets/83a7d747-0603-4c92-802f-fa4949f2b7e7" />

<img width="1210" height="762" alt="image" src="https://github.com/user-attachments/assets/e8f7dff7-7aea-4b70-aa08-ec29e1d9286b" />

<img width="819" height="100" alt="image" src="https://github.com/user-attachments/assets/ebcf6283-2b39-40da-98e4-41a4c9eaf5ed" />

<img width="613" height="51" alt="image" src="https://github.com/user-attachments/assets/cfc9451c-4759-47e9-9ff6-9c5113e5e38e" />
