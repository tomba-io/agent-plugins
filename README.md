<p align="center">
  <a href="https://tomba.io">
    <img src="https://tomba.io/logo.svg" alt="Tomba" width="200">
  </a>
</p>

<h1 align="center">Tomba Agent Plugins</h1>

<p align="center">
  Agent plugins for <a href="https://tomba.io">Tomba</a> remote MCP server — providing email discovery, verification, enrichment, and company research across multiple AI coding assistants.
</p>

<p align="center">
  <a href="https://tomba.io"><img src="https://img.shields.io/badge/Tomba-API-blue?style=flat-square" alt="Tomba API"></a>
  <a href="https://docs.tomba.io/llm/remote-mcp/introduction"><img src="https://img.shields.io/badge/MCP-Supported-green?style=flat-square" alt="MCP Supported"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-yellow?style=flat-square" alt="License: MIT"></a>
  <a href="https://github.com/tomba-io/tomba"><img src="https://img.shields.io/badge/CLI-tomba--io%2Ftomba-orange?style=flat-square" alt="Tomba CLI"></a>
  <img src="https://img.shields.io/badge/Tools-12-purple?style=flat-square" alt="12 Tools">
  <img src="https://img.shields.io/badge/Platforms-7-teal?style=flat-square" alt="7 Platforms">
</p>

---

## Supported Platforms

| Platform                 | Plugin Path         | Auth Method                              |
| ------------------------ | ------------------- | ---------------------------------------- |
| Generic / Multi-agent    | `.agents/plugins/`  | Bearer token or API headers              |
| Claude (Desktop & Code)  | `.claude-plugin/`   | Bearer token                             |
| Cursor AI                | `.cursor-plugin/`   | `X-Tomba-Key` / `X-Tomba-Secret` headers |
| VS Code (GitHub Copilot) | `.vscode/`          | Bearer token (prompted)                  |
| Windsurf                 | `.windsurf-plugin/` | Bearer token                             |
| Zed                      | `.zed-plugin/`      | Bearer token                             |
| ChatGPT (OpenAI API)     | `.chatgpt-plugin/`  | Bearer token                             |

## MCP Server

- **Endpoint**: `https://mcp.tomba.io/mcp`
- **Transport**: Streamable HTTP (JSON-RPC 2.0)
- **Docs**: [docs.tomba.io/llm/remote-mcp/introduction](https://docs.tomba.io/llm/remote-mcp/introduction)

## Available Tools

| Tool                | Description                                  |
| ------------------- | -------------------------------------------- |
| `domain_search`     | Find all emails for a company domain         |
| `email_finder`      | Discover a person's email via name + company |
| `email_verifier`    | Validate email deliverability, MX, SMTP      |
| `email_enrichment`  | Get full contact and company profiles        |
| `email_count`       | Count public emails for a domain             |
| `author_finder`     | Extract author email from article URLs       |
| `linkedin_finder`   | Convert LinkedIn profiles to verified emails |
| `phone_finder`      | Retrieve validated phone numbers             |
| `phone_validator`   | Verify phone numbers with carrier details    |
| `technology_finder` | Identify website technology stacks           |
| `similar_finder`    | Discover competitor/lookalike companies      |
| `companies_search`  | Query company database by attributes         |

All tool definitions are maintained in [`shared/tools.json`](shared/tools.json) as a single source of truth.

## Resources

| Resource     | URI                             | Description                           |
| ------------ | ------------------------------- | ------------------------------------- |
| Account Info | `tomba://account`               | Current account information and usage |
| Domain Stats | `tomba://domain/{domain}/stats` | Email statistics for a domain         |
| Usage Stats  | `tomba://usage`                 | API usage statistics                  |

## Prompts

12 pre-built prompts for common workflows:

| Prompt                    | Description                                                                |
| ------------------------- | -------------------------------------------------------------------------- |
| `lead-research`           | Research a company and find key contacts for outreach                      |
| `competitor-analysis`     | Analyze competitors including tech stack, team structure, and contacts     |
| `email-verification`      | Verify a list of email addresses                                           |
| `find-person`             | Find a specific person's email at a company                                |
| `content-outreach`        | Find authors and content creators for outreach campaigns                   |
| `account-based-marketing` | Build comprehensive ABM campaigns with multi-stakeholder targeting         |
| `investor-research`       | Research VCs/investors, portfolio companies, and find decision makers      |
| `hiring-outreach`         | Source candidates from target companies for recruiting                     |
| `partnership-research`    | Identify strategic partners and integration opportunities                  |
| `market-research`         | Conduct industry analysis across multiple companies                        |
| `sales-territory-mapping` | Build territory plans with account prioritization and stakeholder mapping  |
| `due-diligence`           | Comprehensive company analysis for investment, acquisition, or partnership |

## Authentication

### Option 1: Bearer Token (Recommended)

Encode your credentials as base64:

```bash
echo -n 'ta_your_api_key:ts_your_secret_key' | base64
```

Use the result as:

```
Authorization: Bearer <base64_token>
```

### Option 2: API Headers

```
X-Tomba-Key: ta_your_api_key
X-Tomba-Secret: ts_your_secret_key
```

## Setup

### 1. Get API Credentials

1. Sign up at [app.tomba.io/auth/register](https://app.tomba.io/auth/register)
2. Get your API key (`ta_xxx`) and secret (`ts_xxx`) from [app.tomba.io/api](https://app.tomba.io/api)
3. Copy `.env.example` to `.env` and fill in your credentials

### 2. Configure Your Platform

<details>
<summary><strong>Claude Desktop</strong></summary>

Add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "tomba": {
      "url": "https://mcp.tomba.io/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_BASE64_TOKEN"
      }
    }
  }
}
```

</details>

<details>
<summary><strong>Claude Code</strong></summary>

Run:

```bash
claude mcp add tomba --transport http --url https://mcp.tomba.io/mcp \
  --header "Authorization: Bearer YOUR_BASE64_TOKEN"
```

</details>

<details>
<summary><strong>Cursor AI</strong></summary>

Add to `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "tomba": {
      "url": "https://mcp.tomba.io/mcp",
      "transport": "http",
      "headers": {
        "X-Tomba-Key": "ta_your_api_key",
        "X-Tomba-Secret": "ts_your_secret_key"
      }
    }
  }
}
```

</details>

<details>
<summary><strong>VS Code (GitHub Copilot)</strong></summary>

Add to `.vscode/mcp.json`:

```json
{
  "inputs": [
    {
      "id": "tomba-bearer",
      "type": "promptString",
      "description": "Tomba Bearer Token (base64 of ta_api_key:ts_secret_key)",
      "password": true
    }
  ],
  "servers": {
    "tomba": {
      "type": "http",
      "url": "https://mcp.tomba.io/mcp",
      "headers": {
        "Authorization": "Bearer ${input:tomba-bearer}"
      }
    }
  }
}
```

</details>

<details>
<summary><strong>Windsurf</strong></summary>

Add to Windsurf MCP settings (`~/.codeium/windsurf/mcp_config.json`):

```json
{
  "mcpServers": {
    "tomba": {
      "serverUrl": "https://mcp.tomba.io/mcp",
      "transport": "http",
      "headers": {
        "Authorization": "Bearer YOUR_BASE64_TOKEN"
      }
    }
  }
}
```

</details>

<details>
<summary><strong>Zed</strong></summary>

Add to Zed `settings.json`:

```json
{
  "context_servers": {
    "tomba": {
      "settings": {
        "url": "https://mcp.tomba.io/mcp",
        "headers": {
          "Authorization": "Bearer YOUR_BASE64_TOKEN"
        }
      }
    }
  }
}
```

</details>

<details>
<summary><strong>ChatGPT (OpenAI Responses API)</strong></summary>

Use the MCP tool type in the OpenAI Responses API:

```bash
curl https://api.openai.com/v1/responses \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4.1",
    "tools": [
      {
        "type": "mcp",
        "server_label": "tomba",
        "server_url": "https://mcp.tomba.io/mcp",
        "headers": {
          "Authorization": "Bearer YOUR_TOMBA_BASE64_TOKEN"
        },
        "require_approval": "never"
      }
    ],
    "input": "Find all emails for tomba.io"
  }'
```

</details>

## Tomba CLI

The [Tomba CLI](https://github.com/tomba-io/tomba) provides direct terminal access to the same capabilities.

```bash
# Install
curl -sSL https://releases.tomba.io/install.sh | sh

# Authenticate
tomba login

# Usage
tomba search --target "example.com"
tomba finder --target "example.com" --first "John" --last "Doe"
tomba verify --target "user@example.com"
tomba enrich --target "user@example.com"
tomba linkedin --target "https://linkedin.com/in/profile"
tomba phone-finder --email "user@example.com"
tomba reveal --query "SaaS companies in San Francisco"
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on adding new platform plugins.

## License

[MIT](LICENSE)
