# OverTheWire Bandit Level 2

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | OverTheWire |
| **Challenge Name** | Bandit Level 2 |
| **Category** | Linux Basics |
| **Difficulty** | Easy |
| **Points** | N/A |
| **Author** | OverTheWire |
| **Date Completed** | 2025-08-14 |

## Objective 🎯

The password for the next level is stored in a file called `spaces in this filename` located in the home directory. Another filename challenge! 📁

## Initial Reconnaissance

### Target Information
- **Current User**: bandit2
- **Home Directory**: /home/bandit2
- **Target File**: `spaces in this filename`

### Tools Used
- cat command
- ls command

### Commands/Steps
```bash
ls -la
cat "spaces in this filename"
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
-rw-r--r--  1 root root 3526 May 15  2017 .bashrc
-rw-r--r--  1 root root  675 May 15  2017 .profile
-r--------  1 bandit3 bandit2   33 May  7  2020 spaces in this filename
```

### Step 2: Read the File with Spaces
The filename contains spaces, so we need to quote it or escape the spaces.

**Command/Code:**
```bash
cat "spaces in this filename"
```

**Output:**
```
[REDACTED]
```

## Solution

### Final Answer
The password for bandit3 is stored in the file `spaces in this filename` and can be read using quotes around the filename.

### Complete Walkthrough
1. List directory contents with `ls -la`
2. Notice the file named `spaces in this filename`
3. Use quotes around the filename: `cat "spaces in this filename"`
4. The file contains the password for the next level

## Key Learnings

- Handling filenames with spaces in Linux
- Using quotes to preserve spaces in filenames
- Alternative methods: escaping spaces with backslashes
- Understanding shell interpretation of spaces

## Tools and Resources

### Tools Used
- **cat**: Display file contents
- **ls**: List directory contents

### References
- [OverTheWire Bandit Level 2](https://overthewire.org/wargames/bandit/bandit2.html)


## Tags

`#overthewire` `#bandit` `#linux-basics` `#file-operations` `#beginner`
