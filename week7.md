Security Audit and System Review

In this phase, I carried out a full security audit of the server to evaluate its overall security posture and identify any remaining risks.

I started by installing and running Lynis, which performs a comprehensive system audit covering security configuration, hardening, and compliance checks. The audit confirmed that core security controls such as the firewall, AppArmor, SSH hardening, and automatic updates were in place. Lynis also highlighted general hardening suggestions, which is expected for a non-production virtual machine.

Next, I performed a basic network security assessment using nmap. The scan was run against the server’s IP address to identify exposed services. The results confirmed that only expected services, such as SSH and Apache, were reachable, which matches the configured firewall rules. This indicates that unnecessary network exposure has been minimised.

Access control was verified by checking both AppArmor and UFW. AppArmor was confirmed to be active with multiple profiles enforced, providing application-level access control. The firewall was also active and configured to allow only SSH and Apache traffic, blocking all other inbound connections by default.

I then reviewed all running services using systemctl. Essential services such as SSH, Apache, Fail2Ban, system logging, and networking services were running as expected. No unnecessary or unknown services were identified. Each running service has a clear purpose related to system operation, security, or management, which reduces the attack surface.

Overall, the audit showed that the system is securely configured with layered security controls in place. While no system can be considered completely risk-free, the combination of firewall rules, access controls, intrusion prevention, and regular updates significantly reduces the likelihood and impact of security incidents.
<img width="1063" height="696" alt="image" src="https://github.com/user-attachments/assets/a7f4a4e9-0fa5-4cac-973d-6733d1f2dd31" />
<img width="853" height="667" alt="image" src="https://github.com/user-attachments/assets/a5108be1-c6ad-41d6-a121-6dee1c311bed" />
<img width="1060" height="651" alt="image" src="https://github.com/user-attachments/assets/78a4061b-f928-4a2c-aba3-bcc2601692f2" />
<img width="580" height="72" alt="image" src="https://github.com/user-attachments/assets/499b7262-4d6c-438b-946c-38d6616fc975" />
<img width="805" height="622" alt="image" src="https://github.com/user-attachments/assets/4e0162c0-c6b1-4a5e-9d53-8be390205d7c" />
<img width="567" height="217" alt="image" src="https://github.com/user-attachments/assets/39d298d8-7381-445e-85ae-0c63490c5722" />
<img width="1213" height="679" alt="image" src="https://github.com/user-attachments/assets/4459fd91-b233-49a8-bcd2-ebb827d8262f" />
