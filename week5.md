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
