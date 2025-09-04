# OverTheWire Bandit Level 6

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | OverTheWire |
| **Challenge Name** | Bandit Level 6 |
| **Category** | Linux Basics |
| **Difficulty** | Easy |
| **Points** | N/A |
| **Author** | OverTheWire |
| **Date Completed** | 2025-08-16 |

## Objective 🎯

The password for the next level is stored somewhere on the server and has all of the following properties:
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

## Initial Reconnaissance

### Target Information
- **Current User**: bandit6
- **Home Directory**: /home/bandit6
- **Search Criteria**: File owned by bandit7:bandit6, 33 bytes

### Tools Used
- find command
- cat command

### Commands/Steps
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```

## Methodology

### Step 1: Search for Files with Specific Criteria
Use the `find` command to search the entire filesystem for files matching the criteria.

**Command/Code:**
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

**Output:**
```
/var/lib/dpkg/info/bandit7.password
```

### Step 2: Read the Target File
Read the file that matches all the specified criteria.

**Command/Code:**
```bash
cat /var/lib/dpkg/info/bandit7.password
```

**Output:**
```
[REDACTED]
```

## Solution

### Final Answer
The password for bandit7 is stored in the file `/var/lib/dpkg/info/bandit7.password` which is owned by user bandit7, group bandit6, and is 33 bytes in size.

### Complete Walkthrough
1. Use `find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null` to search the entire filesystem
2. The `2>/dev/null` redirects error messages to suppress permission denied errors
3. The command finds the file `/var/lib/dpkg/info/bandit7.password`
4. Read the file with `cat /var/lib/dpkg/info/bandit7.password`
5. The file contains the password for the next level

## Key Learnings

- Using `find` command to search the entire filesystem
- Understanding file ownership criteria (`-user` and `-group`)
- Using error redirection (`2>/dev/null`) to suppress permission errors
- Searching for files by multiple criteria simultaneously

## Tools and Resources

### Tools Used
- **find**: Search for files with specific criteria
- **cat**: Display file contents

### References
- [OverTheWire Bandit Level 6](https://overthewire.org/wargames/bandit/bandit6.html)


## Tags

`#overthewire` `#bandit` `#linux-basics` `#find-command` `#file-ownership` `#beginner`
