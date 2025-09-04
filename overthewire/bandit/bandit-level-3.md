# OverTheWire Bandit Level 3

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | OverTheWire |
| **Challenge Name** | Bandit Level 3 |
| **Category** | Linux Basics |
| **Difficulty** | Easy |
| **Points** | N/A |
| **Author** | OverTheWire |
| **Date Completed** | 2025-08-14 |

## Objective 🎯

The password for the next level is stored in a hidden file in the `inhere` directory. Time to find those hidden files! 🔍

## Initial Reconnaissance

### Target Information
- **Current User**: bandit3
- **Home Directory**: /home/bandit3
- **Target Directory**: inhere

### Tools Used
- ls command
- cat command

### Commands/Steps
```bash
ls -la
cd inhere
ls -la
cat .hidden
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
-rw-r--r--  1 root root 3526 May 15  2017 .bashrc
-rw-r--r--  1 root root  675 May 15  2017 .profile
drwxr-xr-x  2 root root 4096 May  7  2020 inhere
```

### Step 2: Navigate to inhere Directory
Change to the inhere directory.

**Command/Code:**
```bash
cd inhere
```

### Step 3: List Hidden Files
Use `ls -la` to see hidden files (files starting with a dot).

**Command/Code:**
```bash
ls -la
```

**Output:**
```
total 12
drwxr-xr-x  2 root root 4096 May  7  2020 .
drwxr-xr-x 41 root root 4096 May  7  2020 ..
-rw-r--r--  1 bandit4 bandit3   33 May  7  2020 .hidden
```

### Step 4: Read the Hidden File
Read the contents of the hidden file.

**Command/Code:**
```bash
cat .hidden
```

**Output:**
```
[REDACTED]
```

## Solution

### Final Answer
The password for bandit4 is stored in the hidden file `.hidden` in the `inhere` directory.

### Complete Walkthrough
1. List directory contents with `ls -la`
2. Navigate to the `inhere` directory with `cd inhere`
3. List all files including hidden ones with `ls -la`
4. Read the hidden file with `cat .hidden`
5. The file contains the password for the next level

## Key Learnings

- Understanding hidden files in Linux (files starting with `.`)
- Using `ls -la` to display hidden files
- Directory navigation with `cd`
- File permissions and ownership

## Tools and Resources

### Tools Used
- **ls**: List directory contents
- **cd**: Change directory
- **cat**: Display file contents

### References
- [OverTheWire Bandit Level 3](https://overthewire.org/wargames/bandit/bandit3.html)


## Tags

`#overthewire` `#bandit` `#linux-basics` `#hidden-files` `#beginner`
