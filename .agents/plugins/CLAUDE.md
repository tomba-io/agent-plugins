# Tomba Contact Intelligence - Agent Plugin

## MCP Server

- **Endpoint**: `https://mcp.tomba.io/mcp`
- **Transport**: Streamable HTTP (JSON-RPC 2.0)

## Authentication

### Bearer Token (Recommended)

```
Authorization: Bearer <base64(ta_api_key:ts_secret_key)>
```

### Legacy Headers

```
X-Tomba-Key: ta_your_api_key
X-Tomba-Secret: ts_your_secret_key
```

## Available Tools (12)

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

## Resources (3)

| Resource     | URI                             | Description                           |
| ------------ | ------------------------------- | ------------------------------------- |
| Account Info | `tomba://account`               | Current account information and usage |
| Domain Stats | `tomba://domain/{domain}/stats` | Email statistics for a domain         |
| Usage Stats  | `tomba://usage`                 | API usage statistics                  |

## Prompts (12)

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

## CLI (github.com/tomba-io/tomba)

```bash
# Install
curl -sSL https://releases.tomba.io/install.sh | sh
# or
go install github.com/tomba-io/tomba@latest

# Authenticate
tomba login

# Core commands
tomba search --target "domain.com"
tomba finder --target "domain.com" --first "John" --last "Doe"
tomba verify --target "user@domain.com"
tomba enrich --target "user@domain.com"
tomba linkedin --target "https://linkedin.com/in/profile"
tomba phone-finder --email "user@domain.com"
tomba reveal --query "search terms"
```
