---
title: Agent Finder — Federated Search and Discovery for AI Capabilities
hide:
  - toc
---

# What is Agent Finder?

Agent Finder is an open standard for discovering agent extensibility mechanisms. It enables anyone to build a search engine for skills, MCPs, subagents, and A2A capabilities, making them discoverable to any agent harness—whether it be **Gemini, Claude Code, Copilot, Codex, or Manus**.

[Get Started](why/){: .btn .btn-primary } [Read the Specification](spec/){: .btn .btn-secondary }

---

## Why Agent Finder?

Discovering capabilities to enhance your agent (skills, subagents, hooks) is currently a manual, developer-locked process. With the volume of tools and agents exploding into the millions, sifting through them or pre-installing thousands of integrations is no longer practical. Even with basic search, traditional tool selection degrades in accuracy and latency when context windows are stuffed with thousands of schemas.

### What Agents Should Do
1.  **Global Access**: Access the world's growing catalog of tools and capabilities.
2.  **Zero Prompt Bloat**: Maintain minimal active toolsets to prevent context window degradation.
3.  **Billions-Scale Discovery**: Find the exact tool for the right task out of a catalog of billions.
4.  **Decentralized Trust**: Establish cryptographic trust relationships with authors and sources.
5.  **On-the-Fly Execution**: Install and invoke these capabilities dynamically at runtime.

### What Agent Finder Enables
*   **🔌 Federated Search**: Stand up a decentralized search engine for any agent capability (MCP, skills, A2A, and custom APIs).
*   **🌐 Self-Sovereign Publishing**: Host your standard `ai-catalog.json` at a well-known domain root (`/.well-known/`) to advertise your capabilities.
*   **⚡ Cross-Harness Portability**: Enable any agent from any harness to dynamically discover, verify, and use your tools.

---

## Quick Preview

Here is how a publisher advertises an MCP server using the standard `ai-catalog.json` manifest:

```json
{
  "specVersion": "1.0",
  "host": {
    "displayName": "Acme AI",
    "identifier": "did:web:acme.com"
  },
  "entries": [
    {
      "identifier": "urn:ai:acme.com:agent:trading",
      "displayName": "Finance Trading Agent",
      "type": "application/mcp-server+json",
      "url": "https://api.acme.com/agent.json",
      "representativeQueries": [
        "analyze market trend for 2026"
      ]
    }
  ]
}
```
