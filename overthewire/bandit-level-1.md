# OverTheWire Bandit Level 1

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | OverTheWire |
| **Challenge Name** | Bandit Level 1 |
| **Category** | Linux Basics |
| **Difficulty** | Easy |
| **Points** | N/A |
| **Author** | OverTheWire |
| **Date Completed** | 2025-08-13 |

## Objective 🎯

The password for the next level is stored in a file called `-` located in the home directory. This one was tricky! 🤔

## Initial Reconnaissance

### Target Information
- **Current User**: bandit1
- **Home Directory**: /home/bandit1
- **Target File**: `-` (hyphen)

### Tools Used
- cat command
- ls command

### Commands/Steps
```bash
ls -la
cat -
```

## Methodology

### Step 1: List Directory Contents
First, check what files are in the current directory.

**Command/Code:**
```bash
ls -la
```

**Output:**
```
total 12
drwxr-xr-x  2 root root 4096 May  7  2020 .
drwxrxr-x 41 root root 4096 May  7  2020 ..
-rw-r--r--  1 root root  220 May 15  2017 .bash_logout
-rw-r--r--  1 root root 3526 May 15  2017 .bashrc
-rw-r--r--  1 root root  675 May 15  2017 .profile
-r--------  1 bandit2 bandit1   33 May  7  2020 -
```

### Step 2: Read the File
The file is named `-` (hyphen). To read it, we need to specify the full path or use a special syntax.

**Command/Code:**
```bash
cat ./-
```

**Output:**
```
[REDACTED]
```

## Solution

### Final Answer
The password for bandit2 is stored in the file named `-` and can be read using `cat ./-`.

### Complete Walkthrough
1. List directory contents with `ls -la`
2. Notice the file named `-` (hyphen)
3. Use `cat ./-` to read the file (the `./` prefix tells the shell to treat it as a file, not a command option)
4. The file contains the password for the next level

## Key Learnings

- Understanding special characters in filenames
- Using `./` prefix to distinguish files from command options
- Basic file reading with cat command
- File permissions and ownership

## Tools and Resources

### Tools Used
- **cat**: Display file contents
- **ls**: List directory contents

### References
- [OverTheWire Bandit Level 1](https://overthewire.org/wargames/bandit/bandit1.html)


## Tags

`#overthewire` `#bandit` `#linux-basics` `#file-operations` `#beginner`
