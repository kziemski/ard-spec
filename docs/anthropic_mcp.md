# Anthropic's MCP Registry

!!! danger "TODO: Review Ingestion Theory"
    Guha/Team: Please review the ingestion and superset mapping theory for this ecosystem integration before finalized publication.

Agent Finder acts as an open, protocol-agnostic discovery envelope designed to ingest, wrap, and index the **Model Context Protocol (MCP)** tool ecosystem.

---

## The Envelope Mapping

The Model Context Protocol (MCP) standardizes model-to-data/tool connections. Agent Finder wraps MCP tool server endpoints under the standard `application/mcp-server+json` media type:

```json
{
  "identifier": "urn:ai:acme.com:server:weather",
  "displayName": "Acme Weather Telemetry Server",
  "type": "application/mcp-server+json",
  "url": "https://api.acme.com/mcp/weather.json",
  "capabilities": ["WeatherTool", "ForecastTool"],
  "representativeQueries": [
    "what is the current wind speed in Chicago",
    "get the 5-day forecast for Seattle"
  ]
}
```

---

## Developer Value

*   **Federated Scaling**: Developers of private or enterprise MCP tools can bypass the centralized `modelcontextprotocol.io` registry altogether and host their servers sovereignly on their own FQDNs.
*   **Zero Prompt Bloat**: By indexing `representativeQueries` outside the prompt, clients (like Claude Code) can perform semantic vector searches on the registry first, feeding Claude only the top matching tool schemas dynamically at runtime.
