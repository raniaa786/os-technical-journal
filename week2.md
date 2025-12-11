During Week 2, I focused on understanding the potential security risks to my server and planning how to protect it throughout the rest of the project. Even though this server is running inside VirtualBox, it still needs to be set up properly, just like a real system. The aim this week was not to configure the server yet, but to think ahead about what needs to be secured and how I am going to do it.
1. Understanding the Threats to My System
Even in an isolated virtual environment, several threats still apply. Here are the main security risks I identified:
• Weak or default passwords
Attackers could guess or brute-force the login if I don’t use a strong password or proper authentication.
• Exposed SSH service
SSH is the only way to access the server, which makes it a major point of attack. Things like password authentication, wrong port settings, and unlimited login attempts can be exploited.
• Unpatched or outdated software
If the system is not updated regularly, known vulnerabilities in packages could be used to gain access.
• Misconfigured firewall
Without a firewall, any open service could be accessed unexpectedly. Incorrect rules could expose the system to external traffic.
• Unnecessary services running
Extra services increase the attack surface. A server should only run what it needs.
• Malware or malicious scripts
Even in a VM, downloading untrusted files or enabling unknown repositories can cause compromise.

2. Security Goals for the Project
To protect the server, I set the following key goals:
+ Make SSH access secure
Use key-based authentication instead of passwords
Disable root login
Limit the number of authentication attempts
Potentially move SSH to a non-default port
Use firewall rules to control which connections are allowed
+ Keep the system updated
Enable automatic security updates
Regularly check for new package versions
+ Minimise attack surface
Remove or disable any unused services
Avoid installing unnecessary packages
+ Enforce strong system access controls
Use sudo for privilege management
Follow the principle of least privilege
+ Enable and configure AppArmor
Since Ubuntu uses AppArmor for mandatory access control, I will check its status and ensure it is enforcing profiles.
+ Install Fail2ban later
Fail2ban will help block repeated failed SSH login attempts, adding another layer of protection.

3. Planned Tools and Techniques
In the following weeks, I will be using the tools listed below to meet my security goals:
• UFW (Uncomplicated Firewall)
I will configure UFW to allow only the necessary services (mainly SSH). Everything else will be blocked by default.
• AppArmor
Ubuntu’s mandatory access control system helps contain applications if they become compromised.
• Fail2ban
This will help defend against brute-force attacks by automatically banning IPs that repeatedly fail to log in.
• SSH hardening
I will configure /etc/ssh/sshd_config for more secure access methods.
• Lynis (later in Week 7)
A security auditing tool that will give me a final overview of how secure the system is and what improvements can be made.

4. Why Remote (SSH-only) Administration Matters
SSH-only administration is important because:
-It mirrors how real servers are managed in the industry
-It reduces the attack surface by avoiding graphical tools
-It keeps the environment lightweight and secure
-It forces me to use the command line properly
By not using the VirtualBox GUI at all for server management, I’m keeping the project aligned with real-world best practices.

This week was mainly about planning rather than making changes. I identified the main risks to my server and the tools I will use to protect it. By planning ahead, I now have a clear roadmap for Weeks 3–7, where I will start actually configuring, securing, and testing the system.
