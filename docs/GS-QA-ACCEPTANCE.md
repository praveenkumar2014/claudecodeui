# GS QA Acceptance

- [ ] Clean workspace install, build and typecheck.
- [ ] Existing CloudCLI functions remain operational.
- [ ] Desktop, tablet and mobile layouts have no overflow or unreachable controls.
- [ ] Brand logo, favicon and app icons use supplied GS asset; no borrowed runtime logos presented as GS.
- [ ] Authentication and workspace authorization cover API, socket, project, session and artifact routes.
- [ ] NanoBot and CloudCLI health checks run independently; either can fail without breaking the other.
- [ ] Switching brains keeps session IDs and history isolated.
- [ ] Real runtime chat streams events; no mocked success paths.
- [ ] Cancel/resume behavior verified only where supported.
- [ ] Tool approvals and permissions are enforced server-side.
- [ ] File access and terminal run in isolated workspace sandbox.
- [ ] Git/browser operations and artifacts tested.
- [ ] Secrets never appear in API responses, logs or browser storage.
- [ ] SSRF, path traversal, symlink escape and cross-tenant tests pass.
- [ ] Skill install validates provenance, archive paths and runtime compatibility.
- [ ] Deployment smoke test, backup restore and rollback verified.
- [ ] UI shows capability only when verified by runtime.
- [ ] AGPL/MIT notices and corresponding-source obligations documented.
