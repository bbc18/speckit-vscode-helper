## 2025-02-14 - Fix Command Injection in Git Execution
**Vulnerability:** Found a command injection vulnerability where `childProcess.exec` was used to run `git` commands with user-provided arguments like branch names concatenated into the command string.
**Learning:** Using string concatenation with `childProcess.exec` is dangerous because user input can execute arbitrary shell commands.
**Prevention:** Always use `childProcess.execFile` and pass user inputs as an array of arguments to securely execute external binaries. Additionally, use the `--` separator to prevent option injection when possible.
