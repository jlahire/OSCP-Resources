# OSCP Exam Guide 

[![My Shop](https://img.shields.io/badge/My%20Shop-verylazytech-%23FFDD00?style=flat&logo=buy-me-a-coffee&logoColor=yellow)](https://buymeacoffee.com/verylazytech/extras)
[![Medium](https://img.shields.io/badge/Medium-%40verylazytech-%231572B6?style=flat&logo=medium&logoColor=white)](https://medium.com/@verylazytech)
[![Github](https://img.shields.io/badge/Github-verylazytech-%23181717?style=flat&logo=github&logoColor=white)](https://github.com/verylazytech)
[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-verylazytech-%23FFDD00?style=flat&logo=buy-me-a-coffee&logoColor=yellow)](https://buymeacoffee.com/verylazytech)
[![My GitBook](https://img.shields.io/badge/My%20GitBook-VeryLazyTech-%23FFDD00?style=flat&logo=gitbook&logoColor=white)](https://www.verylazytech.com)
[![X](https://img.shields.io/twitter/url?url=https%3A%2F%2Fx.com%2Fverylazytech)](https://x.com/verylazytech)

> **Important:** Please read this entire document carefully before beginning your exam!

This guide provides essential information on:

- [Exam Structure](#exam-structure)
- [Exam Requirements](#exam-requirements)
- [Exam Information](#exam-information)
- [Submission Instructions](#submission-instructions)
- [Additional Required Information](#additional-required-information)
- [Results](#results)

## Introduction

This guide explains the objectives of the OffSec Certified Professional Plus (OSCP+) certification exam. The guide is divided into three sections:

1. **Section 1**: Requirements for the exam.
2. **Section 2**: Important information and suggestions.
3. **Section 3**: Instructions for after the exam is complete.

The OSCP+ certification exam simulates a live network in a private VPN, which contains a small number of vulnerable machines.

### Exam Details:
- You have **23 hours and 45 minutes** to complete the exam. 
  - If your exam begins at 09:00 GMT, it will end at 08:45 GMT the following day.
- After the exam, you have **24 hours** to upload your documentation.

**Note:** All OSCP exams are proctored. Make sure to read the [proctoring tool learner manual](https://help.offsec.com/hc/en-us/sections/360008126631-Proctored-Exams) and the proctoring FAQ.

## Exam Structure

The OSCP exam machine structure is as follows:

- **3 stand-alone machines (60 points in total):**
  - 20 points per machine
  - 10 points for initial access
  - 10 points for privilege escalation
- **1 Active Directory (AD) set containing 3 machines (40 points in total):**
  - 10 points for machine #1
  - 10 points for machine #2
  - 20 points for machine #3

### Possible Scenarios to Pass (70/100 to pass):
- 40 points AD + 3 local.txt flags (70 points)
- 40 points AD + 2 local.txt flags + 1 proof.txt flag (70 points)
- 20 points AD + 3 local.txt flags + 2 proof.txt flag (70 points)
- 10 points AD + 3 fully completed stand-alone machines (70 points)

### Point Allocation:
- The order in which the exam machines are documented in your report is the order in which they will be graded.
- Points will be awarded for partial and complete administrative control of each machine.
- You must achieve a minimum score of **70 points** to pass the exam, with a maximum of **100 points**.

### Exam Requirements (Section 1)

The specific instructions for each target will be located in your **Exam Control Panel**, which will become available once your exam begins.

### Documentation Requirements:
- You must write a professional report describing your exploitation process for each target.
- The report should include all steps, commands issued, and console output.
- The documentation must be thorough enough for someone to replicate your attacks step-by-step.

**Important:** Insufficient documentation will result in reduced or zero points being awarded.

### Exploit Code:
- If you haven't modified an exploit, provide only the URL where the exploit can be found.
- If you’ve modified an exploit, include:
  - The modified exploit code
  - URL of the original exploit
  - The command used to generate any shellcode (if applicable)
  - Highlighted changes and an explanation of why they were made.

### Exam Proofs:
- Your objective is to exploit each target machine and provide proof of exploitation.
- Each target contains at least one proof file (either **local.txt** or **proof.txt**), which must be retrieved and included in your screenshot.
- Failure to provide these files correctly will result in zero points for the target.

![image](https://github.com/user-attachments/assets/c28ccca8-2aa6-45ab-907b-7db2527f6f30)

### Proof File Requirements:
- For **Windows targets**: A shell with SYSTEM, Administrator, or User with Administrator privileges.
- For **Linux targets**: A root shell is required.

**Screenshot Requirement:** The contents of **local.txt** and **proof.txt** must be shown in a screenshot, which includes the file contents and the IP address of the target using the `ipconfig`, `ifconfig`, or `ip addr` command.

![image](https://github.com/user-attachments/assets/567d4f41-91b1-4b55-a2d3-d3fdba165b81)

## Exam Restrictions

You cannot use the following on the exam:

- Spoofing (IP, ARP, DNS, NBNS, etc.)
- Commercial tools or services (Metasploit Pro, Burp Pro, etc.)
- Automatic exploitation tools (e.g., db_autopwn, SQLmap, etc.)
- Mass vulnerability scanners (e.g., Nessus, OpenVAS, etc.)
- AI Chatbots (OffSec KAI, ChatGPT, etc.)
- Features in other tools that perform similar functions.

### Allowed Tools:
- **Nmap**, **Nikto**, **Burp Free**, **DirBuster**, etc. are allowed for scanning and exploitation.

### Metasploit Restrictions:
- Metasploit and Meterpreter are restricted.
  - You may only use them on **one target machine**. 
  - Once you select your target, Metasploit cannot be used on other machines.
  - Metasploit cannot be used for pivoting.

### Tool Disqualification:
You will be disqualified if you use restricted tools or fail to provide the required proof files correctly. A full list of disqualifications can be found in the **[OSCP Exam FAQ](https://www.offsec.com/legal-docs/)**.

## Exam Information (Section 2)

### Exam Connection:
To connect to the exam environment, you must use **Kali Linux** with **OpenVPN**.

1) Download the exam-connection.tar.bz2 file from the link provided in the exam email to your Kali machine.

2) Extract the file:

```
┌──(kali㉿kali)-[~]
└─$ tar xvfj exam-connection.tar.bz2
OS-XXXXXX-OSCP.ovpn
troubleshooting.sh
```

3) Initiate a connection to the exam lab with OpenVPN:

```
┌──(kali㉿kali)-[~]
└─$ sudo openvpn OS-XXXXXX-OSCP.ovpn
```

4) Enter the username and password provided in the exam email to authenticate to the VPN:

```
┌──(kali㉿kali)-[~]
└─$ sudo openvpn OS-XXXXXX-OSCP.ovpn 1 ⨯
[sudo] password for kali: 
2022-01-11 04:15:50 Note: Treating option '--ncp-ciphers' as '--data-ciphers' (renamed in OpenVPN 2.5).
2022-01-11 04:15:50 OpenVPN 2.5.0 x86_64-pc-linux-gnu [SSL (OpenSSL)] [LZO] [LZ4] [EPOLL] [PKCS11] [MH/PKTINFO] [AEAD] built on Oct 28 2020
2022-01-11 04:15:50 library versions: OpenSSL 1.1.1g 21 Apr 2020, LZO 2.10
🔐 Enter Auth Username: OS-XXXXXX
🔐 Enter Auth Password: *********** 
2022-01-11 04:16:01 TCP/UDP: Preserving recently used remote address: [AF_INET]x.x.x.x:1194
2022-01-11 04:16:01 UDP link local (bound): [AF_INET][undef]:1194
2022-01-11 04:16:01 UDP link remote: [AF_INET]x.x.x.x:1194
2022-01-11 04:16:01 WARNING: this configuration may cache passwords in memory -- use the auth-nocache option to prevent this
2022-01-11 04:16:02 [offensive-security.com] Peer Connection Initiated with [AF_INET]x.x.x.x:1194
2022-01-11 04:16:03 TUN/TAP device tun0 opened
2022-01-11 04:16:03 net_iface_mtu_set: mtu 1500 for tun0
2022-01-11 04:16:03 net_iface_up: set tun0 up
2022-01-11 04:16:03 net_addr_v4_add: 192.168.xx.xx/24 dev tun0
2022-01-11 04:16:03 Initialization Sequence Completed
```
### Exam Control Panel:
Through the **Exam Control Panel**, you can:
- Submit proof files.
- Revert target machines.
- View specific target objectives and point values.

### Machine Reverts:
- You have a limit of **24 reverts**. You can reset the machines once during the exam.

### Proof File Names:
- **proof.txt**: Accessible only to root/Administrator user.
- **local.txt**: Accessible to unprivileged users.

## Submission Instructions

You must submit proof files via the **Exam Control Panel** before your exam ends. The control panel will not indicate if your submission is correct.

## Additional Required Information

For more information on allowed tools, Metasploit restrictions, and submission procedures, please refer to the **[OSCP Exam FAQ](https://help.offsec.com/hc/en-us/sections/360008126631-Proctored-Exams)**.

## Results

After completing your exam and submitting all necessary files, you will receive your results.

---

> **Note:** This is a general guide, and the specific exam details may vary. Always refer to the official [Offensive Security Exam Resources](https://www.offsec.com/legal-docs/) for the most accurate and up-to-date information.
