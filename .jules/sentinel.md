## 2024-05-23 - Prevent Command Injection with execFile
**Vulnerability:** child_process.exec is used with unescaped arguments, allowing command injection via malicious worktree names or branches.
**Learning:** In vscode extensions that work with git paths and branch names, `exec` is dangerous since git repos could be named anything or contain branches with spaces/shell characters.
**Prevention:** Use `child_process.execFile` and pass arguments as an array instead. Ensure `--` is used to separate commands from file paths/branches when calling git.
