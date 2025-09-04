# OverTheWire Bandit Level 4

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | OverTheWire |
| **Challenge Name** | Bandit Level 4 |
| **Category** | Linux Basics |
| **Difficulty** | Easy |
| **Points** | N/A |
| **Author** | OverTheWire |
| **Date Completed** | 2025-08-15 |

## Objective 🎯

The password for the next level is stored in the only human-readable file in the `inhere` directory. Time to analyze file types! 🔬

## Initial Reconnaissance

### Target Information
- **Current User**: bandit4
- **Home Directory**: /home/bandit4
- **Target Directory**: inhere

### Tools Used
- ls command
- file command
- cat command

### Commands/Steps
```bash
ls -la
cd inhere
ls -la
file ./*
cat ./-file07
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

### Step 3: List All Files
List all files in the directory.

**Command/Code:**
```bash
ls -la
```

**Output:**
```
total 48
drwxr-xr-x  2 root root 4096 May  7  2020 .
drwxr-xr-x 41 root root 4096 May  7  2020 ..
-rw-r--r--  1 bandit5 bandit4   33 May  7  2020 -file00
-rw-r--r--  1 bandit5 bandit4   33 May  7  2020 -file01
-rw-r--r--  1 bandit5 bandit4   33 May  7  2020 -file02
-rw-r--r--  1 bandit5 bandit4   33 May  7  2020 -file03
-rw-r--r--  1 bandit5 bandit4   33 May  7  2020 -file04
-rw-r--r--  1 bandit5 bandit4   33 May  7  2020 -file05
-rw-r--r--  1 bandit5 bandit4   33 May  7  2020 -file06
-rw-r--r--  1 bandit5 bandit4   33 May  7  2020 -file07
-rw-r--r--  1 bandit5 bandit4   33 May  7  2020 -file08
-rw-r--r--  1 bandit5 bandit4   33 May  7  2020 -file09
```

### Step 4: Check File Types
Use the `file` command to determine which file is human-readable.

**Command/Code:**
```bash
file ./*
```

**Output:**
```
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```

### Step 5: Read the Human-Readable File
Read the ASCII text file.

**Command/Code:**
```bash
cat ./-file07
```

**Output:**
```
[REDACTED]
```

## Solution

### Final Answer
The password for bandit5 is stored in the file `-file07` which is the only ASCII text file among the binary data files.

### Complete Walkthrough
1. List directory contents with `ls -la`
2. Navigate to the `inhere` directory with `cd inhere`
3. List all files with `ls -la`
4. Use `file ./*` to check file types
5. Identify the ASCII text file (`-file07`)
6. Read the file with `cat ./-file07`
7. The file contains the password for the next level

## Key Learnings

- Using the `file` command to identify file types
- Distinguishing between binary data and ASCII text files
- Understanding file naming conventions with special characters
- Basic file analysis techniques

## Tools and Resources

### Tools Used
- **ls**: List directory contents
- **cd**: Change directory
- **file**: Determine file type
- **cat**: Display file contents

### References
- [OverTheWire Bandit Level 4](https://overthewire.org/wargames/bandit/bandit4.html)


## Tags

`#overthewire` `#bandit` `#linux-basics` `#file-analysis` `#beginner`
