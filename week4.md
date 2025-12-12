This week involved installing the applications I selected in Week 3 and beginning the initial security hardening of my Ubuntu Server. All configuration was performed remotely over SSH, which keeps the environment consistent with real server administration practices.

Installing and checking SSH:
this was already included in my ubuntu server but i checked that the service was running properly with this code:
sudo systemctl statys ssh


<img width="439" height="322" alt="image" src="https://github.com/user-attachments/assets/961b8b49-2c39-4e11-8c41-7dc4ffb8d62c" />

Installing Apache web server:

then i installed apache because I need a real service later on for performance testing and security evaluation. This is the code I used: sudo apt install apache2 -y. I then checked its sstatus using: sudo systemctl status apache2. It was running correctly with no errors.

<img width="606" height="356" alt="image" src="https://github.com/user-attachments/assets/3e0f8744-2194-4980-9861-849696a31682" />

Installing performace and monitering tools:

I installed the tools to generate load and monitor system performance:

-stress-ng: for CPU, RAM and disk stress testing

-htop: for live recourse monitering

-apache2_utils: includes ab which is apache benchmark

i used this command: sudo apt install stress-ng htop apache2_utils -y. As you can see in the screenshot below.

<img width="542" height="350" alt="image" src="https://github.com/user-attachments/assets/324fd84b-1f68-411f-9689-64a29f790d08" />


Configuring the Firewall

To limit access to the server, I enabled UFW and allowed only the two services I actually need right now: SSH and Apache.
Commands:

sudo ufw enable,
sudo ufw allow OpenSSH,
sudo ufw allow 'Apache',
sudo ufw status

The status output showed the rules were added successfully.

<img width="271" height="194" alt="image" src="https://github.com/user-attachments/assets/7baed93b-0fed-4200-ae8a-1d842f2a9e30" />

SSH Hardening

To make the server more secure, I edited the SSH configuration file:

sudo nano /etc/ssh/sshd_config


I changed the following settings:

Disabled root login

Disabled password authentication

Reduced the number of login attempts

These options were updated to:

PermitRootLogin no
PasswordAuthentication no
MaxAuthTries 3


Then I restarted SSH:

sudo systemctl restart sshd

<img width="806" height="614" alt="Screenshot 2025-12-12 214749" src="https://github.com/user-attachments/assets/bd4b9f16-ac71-4e79-a351-fab4a821badc" />

