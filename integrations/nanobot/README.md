# NanoBot Runtime Integration

Repository: https://github.com/HKUDS/nanobot
License: MIT; preserve copyright and license text.

Before implementation, pin a commit and inspect the gateway route registration, WebSocket protocol, auth/token configuration, Python SDK and integration tests. Document exact endpoints, handshake/auth behavior, message schemas, supported cancellation/resume and health checks here. Do not invent REST routes or assume an endpoint merely because it appears in the UI.

Deploy NanoBot as a separate service on an internal network. Do not publish its gateway port directly. The CloudCLI backend adapter must authenticate service-to-service and enforce workspace mapping and authorization.
