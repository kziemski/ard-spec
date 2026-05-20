# Frequently Asked Questions (FAQ)

## Is Agent Finder a replacement for MCP or OpenAPI?

**No.** Agent Finder is a **discovery protocol (an envelope)**, not an execution protocol. It wraps existing execution standards (like MCP, A2A, and OpenAPI) using standard and proposed IANA media types so agents can find them dynamically. Once discovered, the agent connects to the tool using its native protocol (e.g., JSON-RPC for MCP).

---

## How does search work without consuming context window tokens?

Traditional tool selection requires stuffing every available tool schema into the system prompt. Agent Finder moves this calculation outside the LLM into a dedicated search index (`POST /search`). The orchestrator queries the index using natural language, and the index returns only the top 2 or 3 most relevant schemas to inject into the prompt.

---

## Do I need to register my tools on a central directory?

**No.** You have absolute publishing sovereignty. You simply host `ai-catalog.json` on your own domain (`yourdomain.com/.well-known/ai-catalog.json`) to advertise your tools. Any compliant crawler or client can discover and index your endpoint organically without requiring permission.

---

## How do clients securely resolve and verify public keys used in trustManifest signatures?

`TODO(Guha): please fill in`

*   **Context**: The specification defines detached JWS signatures inside the `trustManifest` to verify publisher integrity. However, it does not specify how a client dynamically resolves the public key corresponding to the publisher's `urn:ai:<domain>:...` logical FQDN. 
*   **Proposed Direction**: Define standard DNS-based JWKS endpoint lookups (e.g., `https://domain.com/.well-known/jwks.json`) or align with the `did:web` resolution standard.

---

## How do search registries discover manifest updates without constant polling?

`TODO(Guha): please fill in`

*   **Context**: Static manifests (`/.well-known/ai-catalog.json`) are hosted on publisher domains. If a publisher adds or removes a tool, search registries must discover this update without constant, heavy crawling of millions of FQDNs.
*   **Proposed Direction**: Standardize a lightweight event-driven push specification (such as WebSub or standard webhook registration) to complement pulling.

---

## How does the registry handle cross-protocol deduplication and conflicts?

`TODO(Guha): please fill in`

*   **Context**: If a single tool is packaged as an Open Plugin, an MCP server, and an ACP agent, it may be indexed three times under different identifiers. 
*   **Proposed Direction**: Establish strict logical URN uniqueness rules and define deduplication heuristics based on the underlying endpoint payload hash.
