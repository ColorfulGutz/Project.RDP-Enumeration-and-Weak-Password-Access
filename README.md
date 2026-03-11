# Project.RDP-Enumeration-and-Weak-Password-Access
- A follow along as I utilize labex.io's virtual guided labs

To start off, I test the connectivity of the target system by pinging them, in this lab it is accessible via the hostname target, which I utilize the command `ping` as such, `ping -c 4 target`. This outputs a response showing that my packets did reach them and with 0% packet loss.

<img width="556" height="190" alt="image" src="https://github.com/user-attachments/assets/628147a8-be93-44b4-87b6-7bf4902cede6" />

Next I use nmap to scan the target for any open ports and to identify the services that are running on them. I specifically want to check the RDP service, or Remote Desktop Protocol which is used to remotely control another computer over a network. I accomplish this by running nmap with specific flags to get the desired output, `nmap -sV -p 3389 --script rpd-enum-encryption target`. From the output I can see that port 3389 is open and is running xrdp service, which is the open source implementation of the Remote Desktop Protocol. Although the encryption level is high, that isn't where the main vulnerability lies. Instead it is in the weak password credentials, this is what I intend to exploit.

After insuring that xfreerdp is installed, I use its command line client to try and connect to the target machine, passing a common default for the username and password which is often a primary target for brute force attacks. I do so as such `xfreerdp /u:administrator /p:password /v:target` which asks me to trust the certificate, I input Y and am shown the remote desktop of the victim machine 'target'

<img width="1607" height="895" alt="image" src="https://github.com/user-attachments/assets/5051f482-84c1-4903-8f06-e7d8b5265d58" />

Using their file explorer, Thunar, which is a common file explorer, I search through their home directory, eventually landing on the flag in their Documents folder. To read this, I open the terminal and use cat to output the files contents like so, `cat /home/administrator/Documents/flag.txt`. This then outputs the flag:

<img width="694" height="66" alt="image" src="https://github.com/user-attachments/assets/53f6d1eb-6801-4c00-806e-d7a44a615d3e" />

> Another rather simple lab focusing on exploiting a service against a target machine to capture a flag, more specifically targetting xfreerdp hosted on port 3389 to gain access to the remote system by exploiting a weak, predicatable password for the administrator account.
