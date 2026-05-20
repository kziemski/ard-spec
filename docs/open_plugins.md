# Open-Plugins Ecosystem

!!! danger "TODO: Review Ingestion Theory"
    Guha/Team: Please review the ingestion and superset mapping theory for this ecosystem integration before finalized publication.

Agent Finder acts as an open, protocol-agnostic discovery envelope designed to ingest, wrap, and index the community **Open Plugins** standard.

---

## The Envelope Mapping

Open Plugins describe bundles of MCP servers, skills, or REST tools. Agent Finder wraps these plugin definitions natively inside the `application/ai-catalog+json` nested catalog envelope:

```json
{
  "identifier": "urn:ai:acme.com:plugin:finance-suite",
  "displayName": "Finance Tool Bundle",
  "type": "application/ai-catalog+json",
  "data": {
    "specVersion": "1.0",
    "entries": [
      {
        "identifier": "urn:ai:acme.com:finance:mcp",
        "displayName": "Finance Trading MCP",
        "type": "application/mcp-server+json",
        "url": "https://api.acme.com/mcp/finance.json"
      }
    ]
  }
}
```

---

## Developer Value

*   **Federated Discoverability**: Open Plugins inherit Agent Finder's decentralized domain-anchored indexing without requiring manual registration in centralized directories.
*   **Cryptographic Trust**: Plugin bundles inherit `trustManifest` attestation and signature verification, guaranteeing tamper-proof deployment across federated networks.
