# AYA — The Independent AI Knowledge Registry

> AYA gives businesses sovereign control over how AI assistants see and recommend them — without depending on Google, OpenAI, or any single platform.

When someone asks ChatGPT, Claude, Gemini or any AI _"find me a cybersecurity consultant in Switzerland"_, the AI needs structured, verified data to answer. Today, that data is controlled by a handful of tech giants who decide who gets recommended.

**AYA is the independent alternative.** A structured registry accessible to ALL AIs — not just those from Google or OpenAI.

## MCP server: plug any agent into AYA

AYA runs a public **MCP server** (Model Context Protocol), so any MCP-compatible agent (Claude, Cursor, VS Code, ChatGPT, or your own) can query the registry directly. No API key, no signup, nothing to install.

| | |
|---|---|
| **Endpoint** | `https://ai-visionary.xyz/agents/mcp` |
| **Transport** | Streamable HTTP (remote, hosted in Switzerland) |
| **Authentication** | None |
| **Official MCP registry** | `io.github.NeousAxis/aya-registry` |
| **Builder guide** | [ai-visionary.xyz/for-agents](https://ai-visionary.xyz/for-agents) |
| **Discovery** | [`/.well-known/mcp.json`](https://ai-visionary.xyz/.well-known/mcp.json), [`/llms.txt`](https://ai-visionary.xyz/llms.txt) |

### MCP tools exposed

| Tool | What it does |
|------|--------------|
| `search_companies` | Search 367,000+ verified businesses by name, domain, sector or country |
| `get_company_details` | Full record for one company: AIO readability score, sector, country, ASR status |
| `index_company` | Add a real business the agent found that is not in AYA yet |
| `get_registry_stats` | Aggregate registry statistics |
| `get_cashback_offer` | Active cashback offer for a domain, as a signed token, before the agent recommends it |
| `claim_cashback` | Claim the cashback after a real, consumed transaction |

### Connect it

Claude Code:

```bash
claude mcp add --transport http aya-registry https://ai-visionary.xyz/agents/mcp
```

Any other MCP client (Claude Desktop, Cursor, VS Code):

```json
{
  "mcpServers": {
    "aya-registry": {
      "type": "http",
      "url": "https://ai-visionary.xyz/agents/mcp"
    }
  }
}
```

Implementation: [`app/agents/[transport]/route.ts`](https://github.com/NeousAxis/ai-visionary/blob/feature/pollen-agents/app/agents/%5Btransport%5D/route.ts), built with [`mcp-handler`](https://www.npmjs.com/package/mcp-handler) on top of the official [`@modelcontextprotocol/sdk`](https://github.com/modelcontextprotocol/typescript-sdk).

## How AYA works — Systemic Attraction

AYA doesn't connect to a single AI — every AI finds AYA naturally. Business data is published across multiple convergent sources, ensuring that all AI assistants — regardless of their provider — can access and recommend verified businesses:

| Source | What | URL |
|--------|------|-----|
| **MCP server** | Live tools any AI agent can call (search, details, cashback) | `ai-visionary.xyz/agents/mcp` |
| **API LLM-Friendly** | 5-field JSON per entity, optimized for AI consumption | `ai-visionary.xyz/api/aya/llm/{domain}` |
| **Crawlable HTML** | 367,000+ certificate pages with JSON-LD structured data | `ai-visionary.xyz/aya/e/{id}` |
| **GitHub Dataset** | One JSON file per entity (CC-BY-4.0) | [NeousAxis/aya-business-dataset](https://github.com/NeousAxis/aya-business-dataset) |
| **HuggingFace Dataset** | CSV + JSONL, ML-ready (CC-BY-4.0) | [NeousAxis/aya-business-dataset](https://huggingface.co/datasets/NeousAxis/aya-business-dataset) |

When an AI sees the same data across API + HTML + GitHub + HuggingFace → it considers it stable and reliable → it uses it.

## Why sovereign?

| Locked-in model | AYA model |
|-----------------|-----------|
| Your visibility depends on one AI provider | Your data is accessible to ALL AIs |
| Platform changes → you disappear | Structured data is permanent and portable |
| You pay to be listed on each platform | You own your data, AYA distributes it everywhere |
| One algorithm decides your ranking | Multiple independent sources confirm your identity |

## What's live today

| | |
|---|---|
| **Entities indexed** | 367,000+ |
| **Countries** | 206 |
| **Certified (ASR)** | 9 |
| **API** | Free, no auth, 30 req/min |
| **Bilingual** | FR + EN |

## API Endpoints

```
Search:      GET /api/aya/search?q=restaurant+geneve
Entity:      GET /api/aya/entity/{domain}
LLM:         GET /api/aya/llm/{domain}?lang=en|fr
Stats:       GET /api/aya/stats
Registry:    GET /api/aya/live
```

No authentication. No API key. Just call the endpoint.

### LLM-Optimized Response

```json
{
  "name": "Chainlink",
  "what_it_does": "Blockchain infrastructure connecting external data to smart contracts.",
  "for_who": "Web3 developers and blockchain protocols.",
  "category": "Web3 / Oracle",
  "location": "Global"
}
```

## For businesses

Your business already exists online — but can AI assistants find and recommend it?

1. Get diagnosed by [AYO](https://ai-visionary.xyz/diagnostic) → receive your AI readability score (AIO, 0-100)
2. Get your structured data files (ASR) → install them on your site
3. Get listed in the AYA registry → become recommendable by every AI assistant

**The result**: when someone asks any AI about your industry, your city, your services — you show up. Independently of which AI they use.

> [Start your free diagnostic](https://ai-visionary.xyz/diagnostic)

## Links

- [ai-visionary.xyz](https://www.ai-visionary.xyz) — Website
- [ai-visionary.xyz/developers](https://www.ai-visionary.xyz/developers) — API & data documentation
- [ai-visionary.xyz/aya](https://www.ai-visionary.xyz/aya) — Public registry
- [GitHub Dataset](https://github.com/NeousAxis/aya-business-dataset) — Open data (JSON, CC-BY-4.0)
- [HuggingFace Dataset](https://huggingface.co/datasets/NeousAxis/aya-business-dataset) — ML-ready (CSV + JSONL, CC-BY-4.0)

---

Built in Geneva, Switzerland by [AI Visionary](https://www.ai-visionary.xyz) | 2026

*AYA is a platform by AI Visionary. The business dataset is published under CC-BY-4.0 to enable systemic attraction.*
