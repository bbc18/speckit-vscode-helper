## 2024-03-15 - [Prevent Command Injection via Secure Exec]
**Vulnerability:** Command injection risk identified where user input (branch names, feature folder names, paths) could be passed to the underlying shell through `childProcess.exec`.
**Learning:** `childProcess.exec` is dangerous when combining git commands with variables directly, as it invokes a shell and evaluates the command string.
**Prevention:** Always use `childProcess.execFile` with the arguments split into an array, and use the `--` flag when handling positional branch/file arguments. Never join user input directly into an `exec` string.
