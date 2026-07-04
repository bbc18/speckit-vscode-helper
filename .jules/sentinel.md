## 2026-07-04 - [CRITICAL] Avoiding -- in git rev-parse
**Vulnerability:** Use of `git rev-parse --verify -- <branch>` caused the verification to fail because git interpreted it as a file path instead of a branch/revision.
**Learning:** For git rev-parse --verify, we must omit the `--` separator before the user-supplied branch input.
**Prevention:** Always test child_process.execFile arguments and know exactly which git commands accept `--` as a delimiter and which do not.
