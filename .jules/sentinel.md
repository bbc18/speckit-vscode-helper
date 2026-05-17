## 2026-05-17 - Fix Command Injection in Git Service
**Vulnerability:** Command injection via childProcess.exec string interpolation with unsanitized user inputs (`branch`).
**Learning:** `git rev-parse --verify -- branch` causes a regression in git logic because `--` causes git to expect paths instead of revisions, treating `branch` as a path instead of a revision string.
**Prevention:** Use `childProcess.execFile` with an arguments array, avoiding `--` for revision flags when a branch is expected as a revision argument instead of a path argument (e.g. `git rev-parse --verify <branch>`).
