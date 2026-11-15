# GS Human × AI — Two-Brain Workspace Product Spec

## Scope lock
Only the writable fork `praveenkumar2014/claudecodeui` and the upstream NanoBot source `HKUDS/nanobot` are in scope. No other repositories, projects, domains, hosting deployments or Notion projects.

## Product identity
Use the supplied GS logo PNG/SVG as parent mark. Design two original GS agent identities:
- GS Agent Brain — NanoBot runtime for general assistant, memory, skills, MCP, channels, automation and delegated agents.
- GS Remote Work Brain — CloudCLI runtime for coding agents, remote sessions, terminal, files, editor, Git, browser and project access.
Both are shown inside one branded workspace with explicit runtime distinction. Do not use upstream project marks as GS identity. Preserve upstream attribution and notices.

## User experience
- Responsive GS shell, desktop/tablet/mobile layouts, keyboard support and accessible states.
- Global navigation, workspace/project picker, brain switcher and shared search.
- Agent Brain: streaming chat, tool timeline, approval prompts, attachments, artifacts, history, cancel/resume.
- Remote Work Brain: session/project list, CLI/provider selector, chat, terminal, file tree/editor, Git explorer and browser preview.
- Agent Studio: roles, goals, system instructions, skills, tools/permissions, model/provider, runtime choice, test and package export.
- Skills: versioned SKILL.md packages, provenance and license metadata, adapter/export by runtime.
- Connections: providers, model endpoints, MCP. Secrets write-only and encrypted at rest.
- Operations: service health, runtime versions, queue/run states, failures and audit trail.
Only show capabilities that are verified for the selected runtime; never fake progress, metrics or support.

## Architecture
Keep NanoBot and CloudCLI independent services. CloudCLI fork is the user-facing workspace. NanoBot is a private agent runtime reached through an authenticated backend adapter. CloudCLI keeps its existing coding-agent/session/editor capabilities. Typed adapters normalize shared lifecycle events; runtime-specific IDs remain namespaced. Shared UI must not assume that features are implemented identically.

## Model access
Provider-neutral model configuration for existing CLI account paths where supported, local/self-hosted OpenAI-compatible endpoints, and optional external gateway. No provider is mandatory, no inference is claimed unlimited. Show cost/provider boundary when available. Never store tokens in browser local storage or logs.

## Security baseline
Authentication and workspace authorization on every API/WebSocket route. Secret encryption, audit logs, origin/CSRF protections, rate limits, SSRF prevention, upload limits, secret redaction, workspace-scoped file access and path/symlink protections. All untrusted agent execution isolated in disposable sandboxes/containers with resource quotas and approval gates. Never expose host shell or privileged Docker socket to public-facing agent processes. NanoBot gateway stays on private network.

## Data
Audit existing CloudCLI schema and storage before adding dependencies. Persist user/workspace connections, sessions, run events, approval decisions, skill metadata, audit records and encrypted secrets. Keep runtime state and UI-owned metadata distinct. Provide idempotent migrations, backup and restore.

## License
NanoBot is MIT; retain original copyright/license. CloudCLI is AGPL-3.0-or-later. Preserve license notices and comply with source-disclosure obligations for modified network-hosted/distributed AGPL software. Clearly document modifications and third-party components.
