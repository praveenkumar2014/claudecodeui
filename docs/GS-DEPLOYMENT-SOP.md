# GS Deployment SOP

## Topology
- `gs-workspace`: CloudCLI-derived application, public HTTPS ingress.
- `gs-agent-brain`: NanoBot runtime, private internal network only, persistent volume.
- Database/storage: reuse audited CloudCLI persistence where suitable; do not provision duplicate databases without a documented reason.

## Local development
1. Clone the authorized GS workspace fork.
2. Obtain NanoBot source separately and pin a reviewed commit.
3. Copy `.env.gs.example` to an untracked `.env.gs`; configure random secrets and model provider credentials locally.
4. Build and run separate services using `deploy/docker-compose.gs.yml`.
5. Verify each health endpoint independently before testing adapters.

## Production deployment runbook
1. Provision isolated service identities, network, persistent storage and TLS ingress.
2. Configure secrets through hosting secret manager, never git.
3. Pin source commits and container image digests.
4. Build images and run dependency/license/security scans.
5. Back up database and persistent runtime state.
6. Apply idempotent migrations.
7. Deploy NanoBot privately, verify health/auth, then deploy workspace ingress.
8. Verify login, workspace isolation, both runtime health states, chat, event streaming, cancel, approvals and failure recovery.
9. Verify mobile and desktop responsive views and file/terminal/Git functions inside sandbox.
10. Record deployed commit, image digest, test output, URLs, health checks and operator.
11. Verify backup restore and rollback procedure.

## Rollback
Stop rollout; restore previous immutable image tags and compatible schema snapshot; restore volumes only if migration requires it; verify session integrity and health. Never auto-deploy unrelated domains or projects.

## Compose caveat
The included compose file is a topology template. Confirm the actual NanoBot gateway command, API/WebSocket authentication, health endpoint and Docker build context from the pinned checkout before enabling it in production.
