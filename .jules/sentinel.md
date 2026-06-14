## 2025-06-14 - Fix Command Injection in worktreeService

**Vulnerability:** The application used `child_process.exec` to run Git commands, allowing for potential command injection via the `branch` or `targetPath` arguments in the `addWorktree` function.

**Learning:** When executing external tools like Git, do not use a shell execution environment (`child_process.exec`) with unsanitized arguments. The `exec` function runs a shell, which interprets shell metacharacters and operators, leading to command injection if malicious input is provided.

**Prevention:** Always use `child_process.execFile` (or similar non-shell execution methods like `child_process.spawn`) when executing commands with user-controlled arguments. Pass the executable (`git`) and arguments as a distinct string and array, completely avoiding shell evaluation. Use the `--` separator before positional arguments to prevent argument injection where input might start with `-`.
