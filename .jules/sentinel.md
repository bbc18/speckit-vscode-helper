## 2026-06-22 - Command Injection in Git Execution
**Vulnerability:** Command injection was possible in `worktreeService.ts` and `worktreeAggregator.ts` due to the use of `child_process.exec` to execute Git commands using dynamically concatenated strings (like branch names and directory paths).
**Learning:** This exposes the application if the feature branches or folder names contain shell control characters or argument injection flags.
**Prevention:** Refactored the custom `ExecFn` abstraction to require passing `execFile` arguments as a `ReadonlyArray<string>`. This enforces separation between the base executable (`git`) and its arguments, and avoids shell interpretation. Also used the `--` argument separator to prevent option injection.
