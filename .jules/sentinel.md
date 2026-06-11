## 2024-05-24 - Secure Git Command Execution

**Vulnerability:** Command injection risk due to using `child_process.exec` with string concatenation for git commands and lacking `--` to separate options from user-provided paths/branches.
**Learning:** `child_process.exec` spawns a shell, making it vulnerable to command injection if inputs aren't perfectly sanitized. Furthermore, Git commands can be tricked into interpreting positional arguments (like branch names or paths) as options (e.g. `--help` or `--exec`) if they start with `-`.
**Prevention:** Always use `child_process.execFile` (or similar array-based execution methods) to bypass the shell. Pass arguments as an array. Use the `--` separator before user-controlled positional arguments (like branch names and file paths) to ensure Git treats them strictly as positional arguments, not options. Note: Do not use `--` with `git rev-parse --verify` as it treats the following argument as a file path rather than a branch/revision.
