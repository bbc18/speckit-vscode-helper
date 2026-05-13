## 2026-05-13 - [Command Injection via exec]
**Vulnerability:** childProcess.exec was used with unescaped git inputs (branch, targetPath) directly concatenated into shell strings.
**Learning:** Even internal tool execution requires execFile/spawn over exec, especially when paths or branch names are dynamically generated, to prevent argument/command injection.
**Prevention:** Always use execFile with parameter arrays and use `--` to clearly separate arguments from git subcommands.
