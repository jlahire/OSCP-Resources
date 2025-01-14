# Nmap - Commands

> [!NOTE]
> For VeryLazy hackers use nmapAutomator
> https://github.com/21y4d/nmapAutomator

---------------------------------------------------------------------

## VeryLazyTech WorkFlow
```
nmap <target> -T4                                      # Fast scan to identify open ports quickly only 1000 common ports!
nmap <target> -p-                                      # Scan all ports 1-65,535
nmap <target> -sV -p <port numbers that opend>         # Detects versions of services running on open ports
nmap <target> -sU                                      # Scans for open UDP ports
nmap --script ftp-* <target> -p21                      # Uses Nmap’s scripting engine to check for known vulnerabilities, this is an example for port 21 open and run all scripts of ftp.
nmap -A -p- <target>                                   # Combines OS detection, version detection, script scanning, and traceroute, Notice that it takes time!
```
------------------------------------------------------------------------

# Full Nmap CheatSheet

## Basic Scanning Options

### Ping Scan

```
nmap -sn <target>
```

The -sn flag performs a ping scan to determine if hosts are up.

**Use Case:** Quickly identify live hosts on a network.


### TCP Connect Scan

```
nmap -sT <target>
```

The -sT flag uses the TCP connect method, completing the full three-way handshake.

**Use Case:** Useful when raw packet crafting (e.g., SYN scans) is unavailable due to privilege restrictions.


### SYN Scan (Default)

```
nmap -sS <target>
```

The -sS flag performs a half-open SYN scan, sending SYN packets and waiting for SYN-ACK responses.

**Use Case:** Faster and stealthier than a TCP connect scan, Shows open ports without fully establishing connections.


## Advanced Scanning Techniques

### OS Detection

```
nmap -O <target>
```

The -O flag attempts to identify the operating system of the target by analyzing responses.

**Use Case:** Gain insights into the target’s OS for tailored exploits or patches, Displays probable OS and version information.


### Service Version Detection

```
nmap -sV <target>
```

The -sV flag probes open ports to determine the services running and their versions.

**Use Case:** Identifies vulnerabilities in specific software versions.


## Script Scanning

```
nmap --script <script_name> <target>
```

The --script flag uses Nmap Scripting Engine (NSE) for enhanced scanning functionality.

**Use Case:** Perform specialized tasks like brute-forcing or vulnerability checks.


## UDP Scanning

```
nmap -sU <target>
```

The -sU flag scans for open UDP ports.

**Use Case:** UDP services (e.g., DNS, SNMP) often host critical information.



## Firewall and IDS Evasion

### Evading Firewalls

```
nmap -f -sS -p 80 <target>
```

Fragments packets and performs stealthy SYN scan on port 80.

### Fragmentation

```
nmap -f <target>
```

The -f flag fragments packets to evade detection.
**Use Case:** Bypass firewalls that block large or unfragmented packets.


### Spoofing IP Address

```
nmap -D RND:10 <target>
```

The -D flag uses decoy IPs to mask the real source.

**Use Case:** Confuse intrusion detection systems (IDS).


### Custom Packet Timing

```
nmap --min-rate 1000 <target>
```

The --min-rate flag adjusts the speed of packet transmission.

**Use Case:** Evade detection by IDS through slower or irregular scanning patterns.


## Output Options

### Save to File

```
nmap -oN <file_name> <target>
```

The -oN flag saves output in a human-readable format.

**Use Case:** Save scan results for later review.


### Save in XML

```
nmap -oX <file_name> <target>
```

The -oX flag saves output in XML format.

**Use Case:** Integration with other tools that require structured data.


![image](https://github.com/user-attachments/assets/58c7feb0-b798-43aa-94b7-9a1c17ff2668)



