# OverTheWire Bandit Level 0

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | OverTheWire |
| **Challenge Name** | Bandit Level 0 |
| **Category** | Linux Basics |
| **Difficulty** | Easy |
| **Points** | N/A |
| **Author** | OverTheWire |
| **Date Completed** | 2025-08-13 |

## Objective 🎯

The goal of this level is to log into the game using SSH. The host to which you need to connect is `bandit.labs.overthewire.org`, on port 2220. The username is `bandit0` and the password is `bandit0`.

## Initial Reconnaissance

### Target Information
- **Host**: bandit.labs.overthewire.org
- **Port**: 2220
- **Username**: bandit0
- **Password**: bandit0

### Tools Used
- SSH client

### Commands/Steps
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

## Methodology

### Step 1: Connect to the Server
Connect to the OverTheWire Bandit server using SSH with the provided credentials.

**Command/Code:**
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

**Output:**
```
The authenticity of host '[bandit.labs.overthewire.org]:2220 ([176.9.9.172]:2220)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPujczY.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[bandit.labs.overthewire.org]:2220' (ECDSA key fingerprint) to the list of known hosts.
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit0@bandit.labs.overthewire.org's password: bandit0
```

### Step 2: Verify Connection
Once connected, verify that you're logged in as bandit0 and explore the current directory.

**Command/Code:**
```bash
whoami
pwd
ls -la
```

**Output:**
```
bandit0
/home/bandit0
total 12
drwxr-xr-x  2 root root 4096 May  7  2020 .
drwxr-xr-x 41 root root 4096 May  7  2020 ..
-rw-r--r--  1 root root  220 May 15  2017 .bash_logout
-rw-r--r--  1 root root 3526 May 15  2017 .bashrc
-rw-r--r--  1 root root  675 May 15  2017 .profile
```

## Solution

### Final Answer
Successfully connected to the OverTheWire Bandit server as user `bandit0`.

### Complete Walkthrough
1. Use SSH to connect to bandit.labs.overthewire.org on port 2220
2. Enter username: bandit0
3. Enter password: bandit0
4. Accept the SSH key fingerprint when prompted
5. You are now logged in and ready to proceed to Level 0 → Level 1

## Key Learnings 💡

- Basic SSH connection syntax and usage
- Understanding of non-standard SSH ports
- Introduction to OverTheWire wargames structure
- Basic Linux command navigation (whoami, pwd, ls)

## Tools and Resources

### Tools Used
- **SSH**: Secure Shell protocol for remote access

### References
- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- [SSH Documentation](https://www.openssh.com/manual.html)


## Tags

`#overthewire` `#bandit` `#ssh` `#linux-basics` `#beginner`
