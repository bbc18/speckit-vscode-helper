## 2025-03-05 - [CRITICAL] Prevent Command Injection in Git Executions

**Vulnerability:** A command injection vulnerability was discovered in how the application executes Git commands (`child_process.exec`). Unsanitized branch names and target paths were interpolated into shell strings (e.g., `git worktree add "${targetPath}" "${branch}"`). If an attacker could control these inputs, they could break out of the quotes and execute arbitrary shell commands.
**Learning:** Shell strings using `child_process.exec` are unsafe when concatenating user input. Quotes can be escaped, allowing arbitrary command execution. Additionally, options injections can happen if a user provides an input starting with a hyphen (e.g., `--help`).
**Prevention:**
1. Always prefer `child_process.execFile` or `child_process.spawn` over `child_process.exec`.
2. Pass arguments as an array instead of concatenating them into a single command string, which sidesteps the shell and arguments are passed securely.
3. Use the `--` separator before positional arguments when passing untrusted inputs to CLI tools to ensure they are treated as positional arguments (paths/branches) rather than options (flags).
