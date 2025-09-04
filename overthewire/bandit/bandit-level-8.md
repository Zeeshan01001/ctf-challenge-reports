# OverTheWire Bandit Level 8

## Challenge Information

| Field | Value |
|-------|-------|
| **Platform** | OverTheWire |
| **Challenge Name** | Bandit Level 8 |
| **Category** | Linux Basics |
| **Difficulty** | Easy |
| **Points** | N/A |
| **Author** | OverTheWire |
| **Date Completed** | 2025-08-17 |

## Objective 🎯

The password for the next level is stored in the file `data.txt` and is the only line of text that occurs only once. Time for some text processing! 📝

## Initial Reconnaissance

### Target Information
- **Current User**: bandit8
- **Home Directory**: /home/bandit8
- **Target File**: data.txt
- **Task**: Find the unique line

### Tools Used
- sort command
- uniq command
- cat command

### Commands/Steps
```bash
ls -la
sort data.txt | uniq -u
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
-rw-r--r--  1 bandit9 bandit8 418439 May  7  2020 data.txt
```

### Step 2: Find the Unique Line
Use `sort` and `uniq -u` to find the line that appears only once.

**Command/Code:**
```bash
sort data.txt | uniq -u
```

**Output:**
```
[REDACTED]
```

## Solution

### Final Answer
The password for bandit9 is the unique line found by sorting the data.txt file and using `uniq -u` to display only lines that occur once.

### Complete Walkthrough
1. List directory contents with `ls -la`
2. Notice the large data.txt file (418,439 bytes)
3. Use `sort data.txt | uniq -u` to find the unique line
4. The `sort` command sorts all lines alphabetically
5. The `uniq -u` command shows only lines that appear exactly once
6. The unique line contains the password for the next level

## Key Learnings

- Using `sort` command to sort text data
- Using `uniq` command to find unique or duplicate lines
- Understanding command piping (`|`) to chain commands
- Text processing and data analysis techniques

## Tools and Resources

### Tools Used
- **ls**: List directory contents
- **sort**: Sort lines of text
- **uniq**: Report or filter out repeated lines

### References
- [OverTheWire Bandit Level 8](https://overthewire.org/wargames/bandit/bandit8.html)


## Tags

`#overthewire` `#bandit` `#linux-basics` `#sort` `#uniq` `#text-processing` `#beginner`
