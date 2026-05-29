## 2026-05-28 - Secure Git Command Execution
**Vulnerability:** Command injection risk due to string concatenation in `childProcess.exec` when running Git commands.
**Learning:** In `src/services/worktreeService.ts` and `src/services/worktreeAggregator.ts`, user-supplied branch names and paths were concatenated into strings passed to `childProcess.exec`. `exec` spawns a shell, making it vulnerable to command injection if paths or branch names contain shell metacharacters.
**Prevention:** Replaced `childProcess.exec` with `childProcess.execFile`, changed the `ExecFn` type to accept an array of arguments, and used `--` to separate options from positional arguments (files/branches) to prevent Git from misinterpreting branch names starting with a dash as options.
