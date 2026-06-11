## 2026-06-11 - [Command Injection Prevention in Git Wrappers]
**Vulnerability:** Execution of Git commands using `child_process.exec` in `worktreeService.ts` passed unsanitized arguments directly to a shell wrapper, enabling Command Injection.
**Learning:** Functions that interact with system utilities via arguments formatted dynamically need to avoid shell wrappers to prevent shell metacharacter evaluation.
**Prevention:** Use `child_process.execFile` and pass dynamic values strictly through an `args` array, employing the `--` parameter where relevant to ensure inputs are processed securely as posix arguments rather than commands.
