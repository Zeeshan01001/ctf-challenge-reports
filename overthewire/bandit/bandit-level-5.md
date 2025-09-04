# OverTheWire Bandit Level 5

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | OverTheWire |
| **Challenge Name** | Bandit Level 5 |
| **Category** | Linux Basics |
| **Difficulty** | Easy |
| **Points** | N/A |
| **Author** | OverTheWire |
| **Date Completed** | 2025-08-15 |

## Objective 🎯

The password for the next level is stored in a file somewhere under the `inhere` directory and has all of the following properties:
- human-readable
- 1033 bytes in size
- not executable

## Initial Reconnaissance

### Target Information
- **Current User**: bandit5
- **Home Directory**: /home/bandit5
- **Target Directory**: inhere

### Tools Used
- find command
- ls command
- cat command

### Commands/Steps
```bash
ls -la
cd inhere
find . -type f -size 1033c -executable
find . -type f -size 1033c ! -executable
cat ./maybehere07/.file2
```

## Methodology

### Step 1: List Directory Contents
Check what's in the current directory.

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
drwxr-xr-x  2 root root 4096 May  7  2020 inhere
```

### Step 2: Navigate to inhere Directory
Change to the inhere directory.

**Command/Code:**
```bash
cd inhere
```

### Step 3: List Subdirectories
Check what subdirectories exist.

**Command/Code:**
```bash
ls -la
```

**Output:**
```
total 80
drwxr-xr-x  2 root root 4096 May  7  2020 .
drwxr-xr-x 41 root root 4096 May  7  2020 ..
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere00
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere01
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere02
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere03
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere04
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere05
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere06
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere07
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere08
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere09
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere10
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere11
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere12
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere13
drwxr-xr-x  2 root first 4096 May  7  2020 maybehere14
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere15
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere16
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere17
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere18
drwxr-xr-x  2 root root 4096 May  7  2020 maybehere19
```

### Step 4: Find Files with Specific Criteria
Use the `find` command to locate files that are 1033 bytes and not executable.

**Command/Code:**
```bash
find . -type f -size 1033c ! -executable
```

**Output:**
```
./maybehere07/.file2
```

### Step 5: Read the Target File
Read the file that matches all criteria.

**Command/Code:**
```bash
cat ./maybehere07/.file2
```

**Output:**
```
[REDACTED]
```

## Solution

### Final Answer
The password for bandit6 is stored in the file `./maybehere07/.file2` which is 1033 bytes, human-readable, and not executable.

### Complete Walkthrough
1. List directory contents with `ls -la`
2. Navigate to the `inhere` directory with `cd inhere`
3. List subdirectories with `ls -la`
4. Use `find . -type f -size 1033c ! -executable` to find files matching the criteria
5. Read the found file with `cat ./maybehere07/.file2`
6. The file contains the password for the next level

## Key Learnings

- Using the `find` command with multiple criteria
- Understanding file size specifications (`-size 1033c`)
- Using negation in find commands (`! -executable`)
- Combining file type, size, and permission filters

## Tools and Resources

### Tools Used
- **ls**: List directory contents
- **cd**: Change directory
- **find**: Search for files with specific criteria
- **cat**: Display file contents

### References
- [OverTheWire Bandit Level 5](https://overthewire.org/wargames/bandit/bandit5.html)


## Tags

`#overthewire` `#bandit` `#linux-basics` `#find-command` `#beginner`
