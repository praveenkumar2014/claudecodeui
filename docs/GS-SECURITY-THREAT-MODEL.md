# GS Security Threat Model

## Threats
- Prompt injection leading to shell/file/network side effects.
- Cross-user or cross-workspace access through IDs, paths, sessions or WebSockets.
- Host compromise through direct shell execution or privileged container socket.
- Secret disclosure in logs, prompts, output, browser storage or error traces.
- SSRF through URL fetch, browser, MCP or webhook tools.
- Path traversal and symlink escape from selected project root.
- Malicious skill packages, archives and MCP servers.
- Resource exhaustion from loops, concurrency, oversized uploads or model output.

## Required controls
- Authenticate every API and WebSocket request; authorize owner/workspace on each operation.
- Keep NanoBot gateway private; adapter uses service credentials with least privilege.
- Execute user code only in disposable sandboxes/containers with no privileged host mounts, resource/time limits and explicit network policy.
- Never mount Docker socket into agent workers.
- Approval for shell, destructive file changes, external publishing, email and other side effects.
- Workspace-root enforcement including symlink resolution; reject traversal.
- SSRF deny internal metadata/control-plane addresses and validate redirects/DNS.
- Encrypt secrets at rest; write-only settings; redact logs and traces.
- MCP and skill installation review, package provenance, archive traversal protection.
- Rate limits, upload size/type constraints, audit log, CSRF/origin policy and secure cookies.
- Security tests for cross-workspace IDs, path escape, SSRF, secret redaction and unauthorized tool invocation.

Do not enable public multi-tenant execution until controls are implemented and independently tested.
