## 2024-05-27 - [Command Injection via exec]
**Vulnerability:** child_process.exec allows command injection by running commands within a shell and executing concatenated input (like `branch`).
**Learning:** `git worktree add -b "${branch}" "${targetPath}"` can execute arbitrary code if `branch` or `targetPath` contains shell metacharacters (e.g. `; rm -rf /`). This is highly critical in VSCode extension development since malicious inputs can execute arbitrary commands on the user's host machine.
**Prevention:** Always use `childProcess.execFile` over `childProcess.exec`. Pass positional parameters cleanly in an array, separated by `--` where appropriate, avoiding string interpolation inside shell commands.
