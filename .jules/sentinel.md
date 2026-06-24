
## 2026-06-24 - [CRITICAL] Fix command injection in ExecFn usage
**Vulnerability:** The application used `child_process.exec` to execute shell commands, interpolating paths such as `workspaceRoot` and `targetPath` into the string. This leads to command injection if an attacker can manipulate these directories.
**Learning:** `exec` invokes a shell to evaluate the command string, causing paths with special characters (like semicolons or backticks) to execute arbitrary code. Abstracting `exec` in a generic type (`ExecFn`) without strong argument separation still retains the vulnerability.
**Prevention:** Always use `child_process.execFile` instead of `exec`. Update wrapper signatures (like `ExecFn`) to mandate the separation of the executable string and an array of arguments (`ReadonlyArray<string>`). Never interpolate user-controlled variables into a command string. For `git worktree add`, use `--` to clearly separate branch names and paths so they are not treated as options.
