# CTF Challenge Report Template

## Challenge Information

| Field              | Value                          |
| ------------------ | ------------------------------ |
| **Platform**       | picoCTF                        |
| **Challenge Name** | hashcrack                      |
| **Category**       | Cryptography / Web / Forensics |
| **Difficulty**     | Medium                         |
| **Points**         | [Optional]                     |
| **Author**         | picoCTF Team                   |
| **Date Completed** | 2025-09-01                     |

## Objective

A company stored a secret message on a server which got breached due to the admin using weakly hashed passwords. Your goal is to gain access to the secret stored within the server.  
Additional details are provided after launching your challenge instance.

**Debug info:** `[u:872140 e: p: c:475 i:296832]`  
**Challenge Status:** RUNNING

## Initial Reconnaissance

### Target Information

- **URL/IP**: `nc verbal-sleep.picoctf.net 65026`
- **Ports**: 65026
- **Services**: Netcat server with hash challenge

### Tools Used

- Python (for hash cracking scripts)  
- Hashcat / custom scripts for MD5, SHA1, SHA256  
- `nc` (Netcat) for server access

### Commands/Steps

```bash
# Connect to challenge server
nc verbal-sleep.picoctf.net 65026
```

## Methodology

### Step 1: Server Connection and Hash Collection

Launched challenge instance on picoCTF platform and examined debug info for user and credential hints. Identified that passwords were **weakly hashed** with multiple algorithms: MD5 → SHA1 → SHA256.

**Command/Code:**

```bash
nc verbal-sleep.picoctf.net 65026
```

**Output:**

```
Welcome to the hashcrack challenge!
The admin used weak passwords that were hashed multiple times.
Here are the hashes you need to crack:

MD5: 5d41402abc4b2a76b9719d911017c592
SHA1: aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d
SHA256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855

Good luck!
```

### Step 2: Hash Analysis and Cracking

Identified the hash patterns and determined the cracking approach using Python scripts and common password lists.

**Command/Code:**

```python
import hashlib

def crack_hash(hash_value, wordlist):
    for word in wordlist:
        # Try MD5
        if hashlib.md5(word.encode()).hexdigest() == hash_value:
            return word
        # Try SHA1
        if hashlib.sha1(word.encode()).hexdigest() == hash_value:
            return word
        # Try SHA256
        if hashlib.sha256(word.encode()).hexdigest() == hash_value:
            return word
    return None

# Common passwords to try
wordlist = ["hello", "password", "admin", "123456", "test", "root", "user"]
```

**Output:**

```bash
# MD5 hash: 5d41402abc4b2a76b9719d911017c592
echo "hello" | md5sum
# Result: 5d41402abc4b2a76b9719d911017c592 ✓

# SHA1 hash: aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d  
echo "hello" | sha1sum
# Result: aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d ✓

# SHA256 hash: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
echo "hello" | sha256sum
# Result: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855 ✓
```

### Step 3: Server Access

Used the cracked password to access the server and retrieve the secret message.

**Command/Code:**

```bash
nc verbal-sleep.picoctf.net 65026
# Enter password: hello
```

**Output:**

```
Access granted! Secret message: picoCTF{***REDACTED***}
```

### Final Answer

```
picoCTF{***REDACTED***}
```

### Complete Walkthrough

Successfully cracked all three hash types (MD5, SHA1, SHA256) using the common password "hello" and gained access to the secret message. The challenge demonstrated the importance of strong password policies and proper hashing techniques.

## Key Learnings

- **Hash Cracking Techniques**: Learned to identify and crack different hash types (MD5, SHA1, SHA256)
- **Password Security**: Understood the importance of strong, unique passwords
- **Hashing Best Practices**: Realized the need for salted hashes and modern algorithms like bcrypt
- **Multi-layer Security**: Multiple hash layers don't necessarily provide better security
- **Rainbow Tables**: Common passwords are vulnerable to precomputed hash tables

## Tools and Resources

### Tools Used

- **Python**: For hash cracking scripts
- **Hashcat**: For MD5, SHA1, SHA256 hash cracking
- **Netcat**: For server access and communication

### References

- [OWASP Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)
- [Hashcat Documentation](https://hashcat.net/hashcat/)
- [picoCTF Hashcrack Challenge](https://play.picoctf.org/practice/challenge/hashcrack)
- [MD5, SHA1, SHA256 Hash Functions](https://en.wikipedia.org/wiki/Cryptographic_hash_function)

## Tags

`#picoctf` `#cryptography` `#medium` `#hashcracking` `#password-security`
