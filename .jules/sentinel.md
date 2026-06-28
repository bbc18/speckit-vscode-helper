## 2024-07-28 - Worktree Service Command Injection
**Vulnerability:** child_process.exec is used to run git worktree commands, concatenating user-controlled inputs like branch and targetPath directly into the command string.
**Learning:** This is vulnerable to command injection if branch names or paths are malicious. Even simple features like adding worktrees can open injection vectors if childProcess.exec is used improperly.
**Prevention:** Always use childProcess.execFile for Git commands with arguments passed as an array. Use the '--' separator before paths to prevent parameter injection (treating paths as options).
