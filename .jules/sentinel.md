## 2026-05-22 - Command Injection Prevention in Git Operations
**Vulnerability:** Command injection and argument injection vulnerabilities were present due to the use of `childProcess.exec` passing user-supplied input (e.g., `branch` and `targetPath`) directly into a shell string.
**Learning:** In a codebase frequently executing Git commands with user input, treating arguments as a single shell string is extremely unsafe, even with basic escaping. A project-specific pattern is needed to handle internal tool execution securely.
**Prevention:**
1. Use `childProcess.execFile` over `childProcess.exec` to bypass the shell entirely and pass arguments as an array.
2. For Git operations, use the `--` separator before positional arguments derived from user input to explicitly denote the end of options and prevent argument injection (e.g., when a branch name starts with `-`).
3. Update custom abstraction types like `ExecFn` to enforce this pattern (accepting `file` and `args` array).
