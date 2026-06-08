## 2026-06-08 - Use child_process.execFile to prevent command injection
**Vulnerability:** child_process.exec was used to execute git commands without proper sanitization of arguments like `branch` and `targetPath`.
**Learning:** `exec` spawns a shell and parses the entire string, which is vulnerable to injection if inputs contain shell metacharacters.
**Prevention:** Always use `child_process.execFile` and pass arguments as an array (`args: readonly string[]`), avoiding `--` argument bypasses like using `git rev-parse --verify -- {branch}` which breaks the command.
