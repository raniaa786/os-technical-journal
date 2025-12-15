Task 1: AppArmor Access Control

Ubuntu uses AppArmor as its mandatory access control system. AppArmor works by applying security profiles to applications, which restrict what files, directories, and system resources they are allowed to access.

To check whether AppArmor was enabled on the server, I ran the following command:

sudo aa-status


The output confirmed that the AppArmor kernel module was loaded and that a large number of profiles were active. Many of these profiles were running in enforce mode, which means AppArmor is actively blocking unauthorised actions rather than only logging them.

I then checked the status of the AppArmor service using:

sudo systemctl status apparmor


This showed that the AppArmor service was enabled and active at system startup. This confirms that AppArmor profiles are automatically loaded and applied whenever the server boots.

To show where AppArmor profiles are stored, I listed the contents of the following directory:

ls /etc/apparmor.d/


This directory contains the configuration files for each AppArmor profile. Each profile defines the permissions and restrictions applied to a specific application or service, allowing administrators to control access on a per-application basis.

AppArmor tracks access control activity through system logs, primarily in /var/log/syslog. Any access violations or denied actions are recorded in the logs, which allows administrators to monitor and report on security behaviour without manually inspecting each application.

By verifying that AppArmor is enabled and enforcing security profiles, the server has an additional layer of protection that limits the impact of compromised or misbehaving applications.

<img width="802" height="405" alt="image" src="https://github.com/user-attachments/assets/ceee1e18-e56c-4f84-83b3-038e3fcbf5b9" />

<img width="1219" height="364" alt="image" src="https://github.com/user-attachments/assets/fd7ae908-c73a-4c70-a06f-1a8a5cd80d4c" />

<img width="1090" height="532" alt="image" src="https://github.com/user-attachments/assets/562fa272-ded3-4aea-8fcb-ebd177a31011" />

Task 2: Automatic Security Updates

To reduce the risk of unpatched vulnerabilities, I configured automatic security updates on the Ubuntu Server using the unattended-upgrades package.

I installed the package using the following command:

sudo apt install unattended-upgrades


I then enabled automatic updates by running:

sudo dpkg-reconfigure unattended-upgrades


This configuration ensures that security updates are downloaded and installed automatically without manual intervention. This helps keep the system protected against known vulnerabilities, even if the server is not regularly maintained.

To verify that automatic updates were enabled, I checked the configuration file located at /etc/apt/apt.conf.d/20auto-upgrades. The settings confirmed that package lists are updated automatically and that unattended upgrades are enabled.

Enabling automatic security updates improves the overall security of the server by ensuring critical patches are applied promptly.

<img width="1213" height="445" alt="image" src="https://github.com/user-attachments/assets/746e05ca-f646-4ccc-95b5-74ca1093e204" />

<img width="1203" height="657" alt="image" src="https://github.com/user-attachments/assets/3aaf978f-2e96-45ee-8491-8bd97c091579" />

<img width="610" height="112" alt="image" src="https://github.com/user-attachments/assets/464a9299-c1f8-40ee-97ce-c84120b90b52" />

Task 3: Fail2Ban Configuration

In this task, I installed and configured Fail2Ban to provide additional protection against brute-force attacks on the SSH service.

Fail2Ban works by monitoring log files for repeated failed login attempts. If an IP address exceeds the allowed number of retries, it is automatically blocked for a period of time. This helps protect the server from automated attacks.

I installed Fail2Ban using the system package manager and enabled the service so that it starts automatically at boot. I then created a local configuration file at /etc/fail2ban/jail.local to configure the SSH jail.

In the SSH jail configuration:

The SSH jail was enabled

The SSH port was specified

The system SSH log file was used

The maximum number of failed login attempts was set to 3

After applying the configuration, I restarted the Fail2Ban service and verified that it was running correctly. I confirmed that the SSH jail was active using the Fail2Ban client status command.

This configuration ensures that repeated failed SSH login attempts are automatically detected and blocked, improving the overall security of the server.Fail2Ban will continue running in the background and automatically respond to future failed login attempts without manual intervention.

<img width="1183" height="643" alt="image" src="https://github.com/user-attachments/assets/5e58838e-508b-45d8-8f6d-2a8a7e92557b" />

<img width="1204" height="445" alt="image" src="https://github.com/user-attachments/assets/9f88ca97-5e5b-498b-ad16-5143f6bedbb7" />

<img width="676" height="414" alt="image" src="https://github.com/user-attachments/assets/187343d1-ab19-45ab-ab54-75fbc2044923" />

<img width="1207" height="762" alt="image" src="https://github.com/user-attachments/assets/378e0b38-a421-44c7-9ba4-fb99394f75fc" />

Task 4: Security Baseline Verification Script

For this task, I created a security baseline verification script called security-baseline.sh. The purpose of this script is to check that all the security controls configured in Phase 4 and Phase 5 are correctly applied on the server.

The script is designed to run directly on the server over SSH. When executed, it outputs a clear report showing the current security state of the system. This makes it easy to quickly confirm that key security settings have not been changed or misconfigured.

The script verifies the following security areas:

First, it checks the SSH configuration. It confirms that password authentication is disabled and that root login over SSH is not allowed. These settings help reduce the risk of brute-force attacks and unauthorised access.

Next, the script checks the firewall configuration using UFW. It confirms that the firewall is active and that only the required services, such as OpenSSH and Apache, are allowed through the firewall.

The script then verifies that Fail2Ban is running correctly. It checks that the Fail2Ban service is active and confirms that the SSH jail is enabled. This ensures that repeated failed login attempts are monitored and blocked automatically.

AppArmor is also verified as part of the baseline. The script confirms that AppArmor is loaded and enforcing security profiles, which adds an additional layer of protection by restricting what applications can access on the system.

In addition to this, the script checks whether automatic security updates are enabled using the unattended-upgrades package. This ensures that important security patches are applied automatically without manual intervention.

Finally, the script displays basic system information such as disk usage, memory usage, and users with sudo privileges. This provides extra context about the system state and helps with ongoing monitoring.

By running this script, I can quickly verify that the server remains compliant with the security configuration defined in previous phases. This provides a simple but effective way to validate the security baseline before performance testing and future changes.

Screenshots below show the script permissions, execution, and output confirming that all security controls are active.

<img width="682" height="709" alt="image" src="https://github.com/user-attachments/assets/1ee98edd-dffb-40d6-b8e0-1b286ace88c1" />

<img width="709" height="718" alt="image" src="https://github.com/user-attachments/assets/f5dbe50e-6d66-4038-93a5-74034149a3d7" />

<img width="819" height="475" alt="image" src="https://github.com/user-attachments/assets/323654e2-72c8-4bd1-a5e2-f1ae0f13dc1f" />

Task 5: Remote Server Monitoring Script

In this task, I created a remote monitoring script that connects to the server over SSH and collects basic system and security information. The purpose of this script is to demonstrate how a workstation can remotely monitor a server, rather than logging in manually each time.

I created the script on the workstation and named it monitor-server.sh. The script is designed to connect to the server using SSH and then run common system commands such as checking memory usage, disk usage, and service status. The output is saved to a timestamped log file so that monitoring results can be reviewed later.

When running the script, it correctly attempted to connect to the server using SSH. However, the connection failed. This behaviour is expected based on the security configuration applied earlier in the project.

In Phase 4, password-based SSH authentication was disabled as part of the SSH hardening process. This means the server now only allows SSH access using key-based authentication. Since SSH keys were not yet configured for this monitoring script, the server rejected the connection attempt.

Although the script did not successfully connect, this outcome confirms that the SSH security configuration is working as intended. The server is correctly refusing connections that do not meet the required authentication method. This demonstrates that the system is protected against unauthorised remote access.

In a production environment, this script would be updated to use SSH key-based authentication so that monitoring can run automatically without weakening security. For the purposes of this coursework, the failed connection still provides useful evidence that secure remote access controls are in place and being enforced.

