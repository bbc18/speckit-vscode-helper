## 2026-06-21 - Critical Command Injection fixed

**Vulnerability:** Command injection was present via `childProcess.exec` when user-controlled `branch` strings were passed into the string command passed to it.
**Learning:** Avoid `childProcess.exec` and instead prefer `childProcess.execFile` with separate arguments passed as an array, explicitly separated by `--` where necessary.
**Prevention:** Ensure we always validate and sanitize all inputs, and use parameterized/argument separated tools.
