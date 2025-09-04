# HackTheBox - Irked

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Irked |
| **Category** | Linux Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-25 |

## Objective 🎯

Irked is a Linux machine with multiple services including IRC. The goal is to exploit the services to gain system access and obtain both user and root flags. IRC backdoor exploitation! 💬

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.117
- **OS**: Linux
- **Services**: HTTP, IRC, SSH

### Tools Used
- Nmap
- IRC client
- SSH

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.117
```

## Methodology

### Step 1: Port Scan
```bash
nmap -sC -sV 10.10.10.117
```

### Step 2: IRC Service Enumeration
```bash
nc 10.10.10.117 6697
```

### Step 3: Web Application Enumeration
```bash
curl http://10.10.10.117/
```

### Step 4: Backdoor Exploitation
```bash
nc 10.10.10.117 12345
```

### Step 5: Privilege Escalation
```bash
sudo -l
sudo /usr/bin/view
```

### Step 6: Find Flags
```bash
cat /home/djmardov/user.txt
cat /root/root.txt
```

## Solution

### Final Answer
- **User Flag**: [REDACTED]
- **Root Flag**: [REDACTED]

## Key Learnings

- IRC service exploitation
- Backdoor identification
- View privilege escalation
- Linux system exploitation

## Tags

`#hackthebox` `#linux` `#irc` `#backdoor` `#view` `#easy`
