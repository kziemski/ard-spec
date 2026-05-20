# Zed's ACP Agent Registry

!!! danger "TODO: Review Ingestion Theory"
    Guha/Team: Please review the ingestion and superset mapping theory for this ecosystem integration before finalized publication.

Agent Finder acts as an open, protocol-agnostic discovery envelope designed to ingest, wrap, and index **Zed's Agent Client Protocol (ACP)** capabilities.

---

## The Envelope Mapping

Zed's ACP standardizes editor-to-agent UI integrations. Agent Finder wraps ACP tool endpoints under the proposed `application/acp-agent+json` media type:

```json
{
  "identifier": "urn:ai:acme.com:editor:refactor",
  "displayName": "Acme Workspace Refactoring Agent",
  "type": "application/acp-agent+json",
  "url": "https://api.acme.com/acp/endpoint"
}
```

---

## Developer Value

*   **Cross-Harness Discoverability**: ACP-compliant agents gain permissionless discoverability outside of the Zed editor ecosystem, making them searchable by any harness (e.g., Gemini, Claude Code).
*   **Zero Prompt Bloat**: Editor agents are dynamically searched and loaded into the client's environment only when a workspace refactoring task matches the user's active intent.
