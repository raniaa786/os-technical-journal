This week focused on choosing the applications and system tools that I will install on my Ubuntu Server in later weeks. The goal is to pick software that allows me to test system performance, monitor resource usage, and apply security configurations as required by the coursework.
Even though I am not installing anything yet, planning ahead helps me make sure that my system is set up in a realistic way for the performance testing and security tasks later on.

I selected the following applications to install later in the project:
1. Apache Web Server
I chose Apache because:
-it is one of the most commonly used web servers
-it is easy to configure for testing
-it allows me to generate real network and CPU load
-there is lots of documentation available
Apache will give me something useful to test in Week 6 when I measure performance.

2. OpenSSH Server (already installed)
SSH is the only way I will manage the server, so it remains the key service running throughout the project.
Later, I will harden it by:
-disabling password authentication
-disabling root login
-using key-based authentication
-limiting login attempts
This makes SSH a good application to study from a security perspective.

3. UFW Firewall (planned for Week 4)
UFW will let me control which network ports are open.
It will be used to:
-allow SSH access
-block everything else by default
-protect Apache when it is installed
Even though UFW is not installed yet, it is an important tool for the configuration stage.

4. Performance Testing Tools
These tools will be used during Week 6 to test CPU, disk, memory, and network performance.
• stress-ng
A tool that lets me generate artificial CPU, memory, and I/O load.
Useful for seeing how the server behaves under pressure.
• htop
A real-time system monitor that shows CPU, RAM, and process usage in an easy-to-read layout.
• apache2-utils (ab benchmark tool)
This package includes the ab command, which sends many requests to the web server to measure:
-response time
-throughput
-server capacity
This will help me compare performance before and after security changes.

2. Why I Chose These Applications
I picked applications that are both realistic and easy to work with for learning purposes.
Apache gives me a real service to secure, UFW and SSH allow me to practise server hardening, and the performance tools give me enough data to evaluate the system in Week 6.
I specifically avoided more complex services like databases (MySQL, PostgreSQL) because they are heavier and not required to meet the coursework outcomes.
The combination of Apache + SSH + UFW + stress tools gives me:
-something to secure
-something to measure
-something to test under stress
-something to benchmark
Without making the server too complicated.
