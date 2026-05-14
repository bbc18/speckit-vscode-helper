## 2024-05-14 - Fix Command Injection in WorktreeService
**Vulnerability:** Shell command injection in `worktreeService.ts` because `child_process.exec` was used with shell concatenation for `git worktree add`, enabling execution of arbitrary commands embedded in branch names or paths.
**Learning:** Git operations parsing external input like branch names or paths must never use `child_process.exec`.
**Prevention:** Exclusively use `child_process.execFile` and pass parameters to Git as an array. Use `--` before paths or external arguments to prevent option injection.
