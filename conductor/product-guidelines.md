# Product Guidelines: Local AI Bridge

## Prose & Communication Style
- **Tone:** Professional, direct, and technical. Use an authoritative but helpful tone, suitable for high-level engineering and architecture discussions.
- **Brevity:** Prioritize high signal-to-noise ratio. Avoid conversational filler.
- **Clarity:** Use precise technical terminology (e.g., "SSE," "Chat Completion," "Model Context Protocol").
- **Language:** English (US) for all documentation and code comments.

## Branding & Visual Identity
- **Logo/Iconography:** Use a bridge metaphor combined with AI-related symbols (e.g., neural networks, nodes).
- **Color Palette:** Professional blues, grays, and whites, reflecting an enterprise software aesthetic.
- **Naming:** Always refer to the project as "Local AI Bridge." Avoid acronyms like "LAB" unless used in internal code identifiers.

## UX & Interaction Principles
- **Reliability First:** The bridge must handle connection drops gracefully and provide clear error messages via the MCP protocol.
- **Transparency:** Log all translation steps and API calls (respecting security mandates) to facilitate debugging.
- **Performance:** Optimize the translation layer to introduce minimal overhead.
- **Security:** Rigorously protect API keys and environment variables. Never log sensitive credentials.

## Technical Standards
- **Containerization:** All components must be deployable via Docker.
- **CI/CD:** Every commit must be validated through automated pipelines.
- **Documentation:** Maintain up-to-date Mermaid diagrams for logical and physical architecture in the `README.md`.
