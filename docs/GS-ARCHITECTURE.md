# GS Two-Brain Architecture

## Services
1. `gs-workspace`: modified CloudCLI fork; public HTTPS ingress; frontend and application backend.
2. `gs-agent-brain`: NanoBot service; private network only; persistent data; no public ingress.
3. Optional isolated execution worker/sandbox, only after threat modeling and resource controls.

## Adapter boundary
Define a typed `AgentRuntimeAdapter`:
- identity and capability metadata
- health and version
- create/list/get sessions
- send message and stream normalized events
- cancel/resume run where supported
- list/install skills where supported
- fetch artifacts and status

Implement separate `NanoBotAdapter` and `CloudCliAdapter`. Verify actual upstream API/SDK/WebSocket protocols before coding; don't invent endpoints. Namespace runtime session IDs. Normalize event names: run.started, assistant.delta, assistant.message, tool.started, tool.output, approval.required, artifact.created, run.completed, run.failed, run.cancelled.

## Data/event flow
Browser -> authenticated CloudCLI API -> selected adapter -> private runtime.
Runtime events -> adapter normalization -> per-session event stream -> UI.
Approvals route through workspace policy service, never directly from unauthenticated client to runtime.

## Failure isolation
Either runtime may be offline independently. Workspace still loads and displays runtime health. Retry and timeout behavior must not corrupt or merge session histories.
