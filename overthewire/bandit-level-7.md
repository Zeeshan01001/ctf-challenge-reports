# OverTheWire Bandit Level 7

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | OverTheWire |
| **Challenge Name** | Bandit Level 7 |
| **Category** | Linux Basics |
| **Difficulty** | Easy |
| **Points** | N/A |
| **Author** | OverTheWire |
| **Date Completed** | 2025-08-16 |

## Objective 🎯

The password for the next level is stored in the file `data.txt` next to the word `millionth`. Time to search through a big file! 🔍

## Initial Reconnaissance

### Target Information
- **Current User**: bandit7
- **Home Directory**: /home/bandit7
- **Target File**: data.txt
- **Search Term**: millionth

### Tools Used
- grep command
- cat command

### Commands/Steps
```bash
ls -la
grep millionth data.txt
```

## Methodology

### Step 1: List Directory Contents
Check what files are in the current directory.

**Command/Code:**
```bash
ls -la
```

**Output:**
```
total 12
drwxr-xr-x  2 root root 4096 May  7  2020 .
drwxr-xr-x 41 root root 4096 May  7  2020 ..
-rw-r--r--  1 root root  220 May 15  2017 .bash_logout
-rw-r--r--  1 root root 3526 May  7  2020 .bashrc
-rw-r--r--  1 root root  675 May 15  2017 .profile
-rw-r--r--  1 bandit8 bandit7 411741 May  7  2020 data.txt
```

### Step 2: Search for the Word "millionth"
Use `grep` to search for the word "millionth" in the data.txt file.

**Command/Code:**
```bash
grep millionth data.txt
```

**Output:**
```
millionth       [REDACTED]
```

## Solution

### Final Answer
The password for bandit8 is found next to the word "millionth" in the data.txt file using the grep command.

### Complete Walkthrough
1. List directory contents with `ls -la`
2. Notice the large data.txt file (411,741 bytes)
3. Use `grep millionth data.txt` to search for the word "millionth"
4. The grep command returns the line containing "millionth" followed by the password
5. The password is the value next to "millionth"

## Key Learnings

- Using `grep` command to search for text patterns in files
- Understanding text search and pattern matching
- Working with large files efficiently
- Basic text processing in Linux

## Tools and Resources

### Tools Used
- **ls**: List directory contents
- **grep**: Search for text patterns in files

### References
- [OverTheWire Bandit Level 7](https://overthewire.org/wargames/bandit/bandit7.html)


## Tags

`#overthewire` `#bandit` `#linux-basics` `#grep` `#text-search` `#beginner`
