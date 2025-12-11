1. System Architecture Overview

For this project, I am using a simple two-system setup:

my workstation (the machine I use to control everything), and

a server virtual machine running Ubuntu Server 22.04 LTS, set up without a graphical interface.

All of the work on the server is done remotely over SSH, which runs through a VirtualBox Host-Only Network. This means the server is completely isolated and only accessible from my workstation. It also forces me to rely on the command line, which is exactly what the module expects.

![System Architecture Diagram](https://github.com/user-attachments/assets/927aa484-777c-4ac6-994f-1da623abbbbd)

This architecture is similar to how real servers are managed in industry: you normally don’t touch the server directly — you connect to it remotely. Using SSH for everything also helps me practise core Linux administration skills.

I chose Ubuntu Server 22.04 LTS mainly because I wanted something reliable and familiar. Ubuntu is very widely used, and although a lot of students will also pick it, I decided it was still the best option for me for a few reasons:

I’ve used Ubuntu before, so I already understand the basics and wouldn’t waste time dealing with unfamiliar tools.

Ubuntu Server is lightweight and doesn’t come with a desktop environment, which is perfect for a headless setup.

It includes the option to enable OpenSSH Server during installation, which saves time and avoids extra configuration steps.

There is a huge amount of documentation online, which is useful when I get stuck.

The LTS version receives long-term security updates, so it’s stable and predictable.

Even though many students may choose Ubuntu, it made sense for me because I want to focus on actually understanding the security, system configuration, and performance testing parts of the coursework instead of struggling with the OS itself.

Comparison with Alternatives:

Fedora Server: More cutting-edge but updates very frequently, which sometimes causes issues. It also uses SELinux heavily, which can be confusing.

Debian: Extremely stable but software versions are often older.

CentOS/AlmaLinux: Stable and enterprise-focused, but not as beginner-friendly as Ubuntu.

For my situation, Ubuntu provided the right balance of simplicity, reliability, and good documentation.

Workstation Configuration:
For the workstation, I decided to use my host machine rather than another virtual machine. My host already has an SSH client installed, and this setup is lighter on my computer since I only need to run one VM instead of two.

All server tasks (like updates, configuration, and monitoring) will be done through SSH, not from the VirtualBox console. This keeps the setup closer to a real-world environment.

Network Configuration:
I set up the server VM to use a VirtualBox Host-Only Adapter. This type of network is completely isolated, which means:
-only my workstation can reach the server
-I can safely use tools like nmap without affecting anything outside my VM
-the server is not exposed to the internet
Network Details:
-Adapter: Host-Only Network
-Server IP: something like 192.168.56.xxx (assigned automatically or manually)
-Subnet: 255.255.255.0
-Gateway: none (because this network is isolated)
-Purpose: SSH communication only
This setup makes testing safer and avoids any accidental interaction with real external systems.

## System Specification Screenshots

### Kernel and OS info, memory usage, and disk space:
![System screenshot](https://github.com/user-attachments/assets/96ccf062-8f17-4766-8055-43ee546e75ea)

### Network interfaces and Ubuntu release details:
![Network and release details](https://github.com/user-attachments/assets/645c4488-cafa-410a-837d-45f81953dea0)
