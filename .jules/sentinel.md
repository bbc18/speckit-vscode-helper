## 2026-06-09 - [Child Process Execution Injection Fix]
**Vulnerability:** Use of `child_process.exec` in `worktreeService.ts` and `worktreeAggregator.ts` for executing Git commands, leaving the extension vulnerable to command injection and argument injection through branch names or paths.
**Learning:** By wrapping `child_process.exec` we created a potential vector for shell command injection. `git rev-parse --verify "${branch}"` can easily be broken if `branch` contains `"` or other shell metacharacters.
**Prevention:** Use `child_process.execFile` instead, pass arguments as an array, and use `--` to separate options from paths/references where appropriate.
