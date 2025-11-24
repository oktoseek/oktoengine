# Contributing to OktoEngine

Thank you for your interest in OktoEngine! 🐙

**OktoEngine** is a proprietary CLI engine developed by **OktoSeek AI**. While the source code is not open source, we welcome feedback, bug reports, and feature requests from the community.

---

## How to Contribute

### Reporting Bugs

If you find a bug, please open an issue on GitHub with:

- **Clear description** of the problem
- **Steps to reproduce** the issue
- **Expected vs actual behavior**
- **OktoEngine version:** `okto --version`
- **System information:** `okto doctor` output
- **Debug output** (if applicable): `okto <command> --debug`

**Example:**
```
Bug: Training fails with "Model not found" error

Steps to reproduce:
1. Run `okto init test-project`
2. Edit scripts/train.okt with MODEL { base: "invalid-model" }
3. Run `okto train`

Expected: Clear error message about invalid model
Actual: Generic "Model not found" error

Version: okto 0.1.0
System: Windows 10, GPU: RTX 4070
```

### Feature Requests

Have an idea for a new feature? Open an issue with:

- **Feature description** - What you'd like to see
- **Use case** - Why this feature would be useful
- **Proposed implementation** (optional) - How you think it could work

### Documentation Improvements

Found an error in the documentation? Want to add examples or clarify something?

- Open an issue describing the improvement
- Or submit a pull request with documentation changes (if applicable)

### Examples

Have a great example project? Share it!

- Create an issue with your example
- Include your `train.okt` file
- Describe what your example demonstrates

---

## Code Contributions

**Note:** OktoEngine source code is proprietary. However, we may accept contributions for:

- Documentation improvements
- Example projects
- Test cases
- Bug fixes (in specific cases)

If you're interested in contributing code, please contact us first at **service@oktoseek.com**.

---

## Reporting Security Issues

**Please do not report security vulnerabilities publicly.**

If you discover a security issue, please email **security@oktoseek.com** with:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested fix (if any)

We will respond promptly and work with you to resolve the issue.

---

## Code of Conduct

### Our Standards

- Be respectful and inclusive
- Welcome newcomers and help them learn
- Focus on constructive feedback
- Respect different viewpoints and experiences

### Unacceptable Behavior

- Harassment or discrimination
- Trolling or inflammatory comments
- Personal attacks
- Publishing others' private information

---

## Questions?

- **GitHub Issues:** https://github.com/oktoseek/oktoengine/issues
- **Email:** service@oktoseek.com
- **Website:** https://www.oktoseek.com

---

**OktoEngine** is developed and maintained by **OktoSeek AI**.

Thank you for helping make OktoEngine better! 🚀

