# GS Runtime Adapter API Contract

This is the target internal contract, not a statement that either upstream runtime already exposes these exact endpoints.

```ts
type RuntimeCapability =
  | "chat" | "streaming" | "sessions" | "cancel"
  | "resume" | "skills" | "mcp" | "terminal"
  | "files" | "git" | "browser" | "artifacts";

type RuntimeEvent =
  | { type: "run.started"; runId: string; sessionId: string }
  | { type: "assistant.delta"; runId: string; text: string }
  | { type: "assistant.message"; runId: string; messageId: string; text: string }
  | { type: "tool.started"; runId: string; tool: string; callId: string }
  | { type: "tool.output"; runId: string; callId: string; output: unknown }
  | { type: "approval.required"; runId: string; approvalId: string; summary: string }
  | { type: "artifact.created"; runId: string; artifactId: string; name: string }
  | { type: "run.completed" | "run.failed" | "run.cancelled"; runId: string; reason?: string };

interface AgentRuntimeAdapter {
  readonly id: string;
  readonly displayName: string;
  readonly capabilities: ReadonlySet<RuntimeCapability>;
  health(): Promise<{ ok: boolean; version?: string; detail?: string }>;
  listSessions(workspaceId: string): Promise<unknown[]>;
  createSession(input: { workspaceId: string; projectId?: string }): Promise<{ sessionId: string }>;
  sendMessage(input: { sessionId: string; text: string }): Promise<{ runId: string }>;
  streamEvents(runId: string, signal?: AbortSignal): AsyncIterable<RuntimeEvent>;
  cancelRun(runId: string): Promise<void>;
  resumeRun(runId: string): Promise<void>;
  listSkills(): Promise<unknown[]>;
  installSkill(skillId: string): Promise<void>;
  getArtifacts(runId: string): Promise<unknown[]>;
}
```

Methods unsupported by a runtime must return explicit unsupported errors and be omitted from UI capability display. Auth and workspace authorization must happen before adapter calls.
