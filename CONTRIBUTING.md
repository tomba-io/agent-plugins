# Contributing to Tomba Agent Plugins

Thanks for your interest in contributing! This guide will help you add new platform plugins or improve existing ones.

## Project Structure

```
agent-plugins/
├── shared/
│   └── tools.json              # Shared tool definitions (single source of truth)
├── .agents/plugins/            # Generic multi-agent plugin
├── .claude-plugin/             # Claude Desktop & Code plugin
├── .cursor-plugin/             # Cursor AI plugin
├── .windsurf-plugin/           # Windsurf plugin
├── .zed-plugin/                # Zed editor plugin
├── .chatgpt-plugin/            # ChatGPT / OpenAI plugin
├── .vscode/                    # VS Code / GitHub Copilot config
├── .env.example                # Environment variable template
├── LICENSE                     # MIT License
└── README.md                   # Documentation
```

## Adding a New Platform Plugin

1. **Create a directory** named `.{platform}-plugin/`
2. **Create `tomba-mcp.json`** inside it with the platform-specific MCP config
3. **Reference `shared/tools.json`** for tool definitions — do not duplicate schemas
4. **Include platform-specific fields** (auth format, transport, headers)
5. **Update `README.md`** with the new platform in the Supported Platforms table and setup instructions
6. **Test the configuration** on the actual platform before submitting

## Plugin Config Template

Every plugin should include at minimum:

```json
{
  "name": "tomba-contact-intelligence",
  "version": "1.0.0",
  "description": "Tomba Contact Intelligence MCP plugin for {Platform}",
  "mcpServers": {
    "tomba": {
      "url": "https://mcp.tomba.io/mcp",
      "headers": {}
    }
  },
  "tools_ref": "../shared/tools.json",
  "setup": {
    "instructions": []
  }
}
```

## Guidelines

- Keep tool definitions in `shared/tools.json` — platform plugins should reference, not duplicate
- Use the platform's native auth pattern (Bearer token, API headers, input prompts, etc.)
- Include setup instructions specific to the platform
- Test with real Tomba API credentials before submitting
- Follow the existing JSON formatting style (2-space indentation)

## Updating Tool Definitions

If Tomba adds new MCP tools or changes parameters:

1. Update `shared/tools.json` first
2. Verify each platform plugin still works
3. Update `README.md` tool table if needed

## Submitting Changes

1. Fork the repository
2. Create a feature branch: `git checkout -b add-{platform}-plugin`
3. Make your changes
4. Test on the target platform
5. Submit a pull request with a clear description

## Questions?

- Tomba API docs: https://docs.tomba.io
- MCP docs: https://docs.tomba.io/llm/remote-mcp/introduction
- Issues: Open a GitHub issue
