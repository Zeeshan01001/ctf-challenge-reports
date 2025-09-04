# Contributing to CTF Challenges Reports

Thank you for your interest in contributing to this CTF challenges repository! This document provides guidelines for adding new reports and maintaining consistency across the project.

## 📋 Table of Contents

- [Getting Started](#getting-started)
- [Report Guidelines](#report-guidelines)
- [Directory Structure](#directory-structure)
- [Templates](#templates)
- [Code Style](#code-style)
- [Screenshots and Media](#screenshots-and-media)
- [Pull Request Process](#pull-request-process)

## 🚀 Getting Started

1. **Fork the repository** on GitHub
2. **Clone your fork** locally
3. **Create a new branch** for your contribution
4. **Follow the guidelines** below for adding reports

## 📝 Report Guidelines

### Required Information
Every CTF report must include:

- **Challenge metadata** (platform, name, category, difficulty)
- **Clear objective** statement
- **Step-by-step methodology**
- **Tools and commands used**
- **Final solution/flag**
- **Key learnings and takeaways**

### Report Quality Standards

#### ✅ Do:
- Use clear, descriptive language
- Include all relevant commands and outputs
- Explain the reasoning behind each step
- Add screenshots for complex steps
- Use proper markdown formatting
- Include relevant tags and categories
- Test all commands before documenting

#### ❌ Don't:
- Include actual flags in public repositories (use `[REDACTED]` or `[FLAG]`)
- Copy solutions without understanding them
- Use offensive or inappropriate language
- Include personal information or credentials
- Submit reports for challenges you haven't completed

## 📁 Directory Structure

Organize reports by platform and difficulty:

```
platform/
├── beginner/
│   ├── challenge-name.md
│   └── another-challenge.md
├── intermediate/
│   └── challenge-name.md
└── advanced/
    └── challenge-name.md
```

### Naming Convention
- Use lowercase with hyphens: `sql-injection-basics.md`
- Be descriptive but concise
- Include platform prefix if needed: `thm-basic-pentesting.md`

## 📋 Templates

### Full Report Template
Use `templates/ctf-report-template.md` for comprehensive writeups.

### Quick Writeup Template
Use `templates/writeup-template.md` for brief solutions.

### Template Usage
1. Copy the appropriate template
2. Fill in all sections
3. Remove sections that don't apply
4. Maintain consistent formatting

## 💻 Code Style

### Command Blocks
```bash
# Always include comments explaining what commands do
nmap -sC -sV target_ip
```

### Code Formatting
- Use proper syntax highlighting
- Include relevant comments
- Show both input and output when helpful
- Use consistent indentation

### File Paths
- Use forward slashes: `/path/to/file`
- Use relative paths when possible
- Quote paths with spaces: `"path with spaces/file"`

## 📸 Screenshots and Media

### Screenshot Guidelines
- Use clear, high-quality images
- Crop to relevant content
- Include captions when helpful
- Store in `assets/images/` directory

### File Naming
- Use descriptive names: `nmap-scan-results.png`
- Include platform prefix: `thm-web-exploitation.png`
- Use lowercase with hyphens

### Privacy and Security
- Blur or redact sensitive information
- Don't include personal data
- Remove any credentials or tokens

## 🔄 Pull Request Process

### Before Submitting
1. **Test your report** - ensure all commands work
2. **Check formatting** - use markdown linting tools
3. **Review content** - proofread for clarity and accuracy
4. **Update documentation** - add to relevant index files

### PR Description Template
```markdown
## Description
Brief description of the challenge and solution.

## Platform
- [ ] TryHackMe
- [ ] picoCTF
- [ ] OverTheWire
- [ ] HackTheBox
- [ ] Other

## Category
- [ ] Web
- [ ] Crypto
- [ ] Forensics
- [ ] Reverse Engineering
- [ ] Pwn
- [ ] Misc

## Changes Made
- Added new challenge report for [challenge name]
- Included step-by-step methodology
- Added screenshots and code examples

## Testing
- [ ] All commands tested and working
- [ ] Screenshots verified
- [ ] No sensitive information included
```

### Review Process
1. **Automated checks** - formatting and basic validation
2. **Content review** - accuracy and completeness
3. **Technical review** - command verification
4. **Final approval** - merge to main branch

## 🏷️ Tagging System

Use consistent tags for better organization:

### Platforms
- `#tryhackme` `#picoctf` `#overthewire` `#hackthebox`

### Categories
- `#web` `#crypto` `#forensics` `#reverse-engineering` `#pwn` `#misc`

### Difficulty
- `#beginner` `#intermediate` `#advanced` `#expert`

### Tools
- `#nmap` `#burp-suite` `#john` `#hashcat` `#metasploit`

### Techniques
- `#sql-injection` `#xss` `#buffer-overflow` `#privilege-escalation`

## 📚 Resources

### Documentation
- [Markdown Guide](https://www.markdownguide.org/)
- [GitHub Flavored Markdown](https://github.github.com/gfm/)

### Tools
- [Markdown Lint](https://github.com/markdownlint/markdownlint)
- [Typora](https://typora.io/) - Markdown editor
- [Screenshots](https://www.screentogif.com/) - GIF creation

### CTF Platforms
- [TryHackMe](https://tryhackme.com/)
- [picoCTF](https://picoctf.org/)
- [OverTheWire](https://overthewire.org/)
- [HackTheBox](https://www.hackthebox.com/)

## 🤝 Community Guidelines

### Be Respectful
- Use inclusive language
- Be constructive in feedback
- Help others learn and grow

### Share Knowledge
- Explain concepts clearly
- Provide additional resources
- Encourage questions and discussion

### Maintain Quality
- Double-check your work
- Follow established patterns
- Continuously improve

## 📞 Getting Help

If you need assistance:

1. **Check existing issues** on GitHub
2. **Create a new issue** with detailed description
3. **Join discussions** in the community
4. **Ask questions** in pull request comments

## 📄 License

By contributing to this project, you agree that your contributions will be licensed under the same license as the project.

---

**Thank you for contributing to the cybersecurity learning community! 🚀**
