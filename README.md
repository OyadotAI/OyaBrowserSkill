# Oya Browser Skill

Teach any AI agent how to control a real browser through [Oya Browser](https://browser.oya.ai) MCP tools.

Built by [Oya.ai](https://oya.ai) — building reliable AI employees that can browse, act, and get work done on the real web.

## Install the skill

```bash
npx skills add OyadotAI/OyaBrowserSkill
```

## Setup

### 1. Download Oya Browser

Get it from [browser.oya.ai](https://browser.oya.ai/#download) — available for macOS and Linux.

### 2. Get your API key

Go to the [dashboard](https://browser.oya.ai/dashboard), sign up, and create an API key.

### 3. Connect the browser

Open Oya Browser. Enter the server URL and your API key:

- **Server URL**: `wss://browser.oya.ai/ws`
- **API Key**: paste your key from step 2

Your browser should appear in the dashboard.

### 4. Add the MCP server to your agent

Go to the **MCP tab** in the dashboard to get your config. Add it to your agent:

**Claude Code** (`~/.claude.json` or project `.mcp.json`):
```json
{
  "mcpServers": {
    "oya-browser": {
      "url": "https://browser.oya.ai/mcp/YOUR_BROWSER_ID",
      "transport": "streamable-http",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

**Cursor** (`.cursor/mcp.json`):
```json
{
  "mcpServers": {
    "oya-browser": {
      "url": "https://browser.oya.ai/mcp/YOUR_BROWSER_ID",
      "transport": "streamable-http",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

**Pool mode** (round-robin across multiple browsers):
```json
{
  "mcpServers": {
    "oya-browser": {
      "url": "https://browser.oya.ai/mcp/pool",
      "transport": "streamable-http",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

### 5. Install the skill

```bash
npx skills add OyadotAI/OyaBrowserSkill
```

### 6. Start using it

Ask your agent to browse the web:

> "Go to Hacker News and find the top post about AI"

> "Log into LinkedIn and check my notifications"

> "Search Amazon for wireless headphones under $50"

The skill teaches the agent the workflow: navigate → analyze page → act by element ID → re-analyze.

## What it does

This skill gives LLMs the mental model and strategies to effectively browse the web using Oya Browser. Instead of fighting raw HTML, CSS selectors, or pixel coordinates, the agent works with structured markdown and numbered element IDs:

```
[#9 input:text placeholder="Search"]   →   type(9, "query")
[#13 button "Google Search"]           →   click(13)
```

## What the agent learns

- **Workflow**: analyze → act → re-analyze loop
- **17 tools**: element clicks, coordinate clicks, mouse move, double click, drag, keyboard type, scroll, screenshots, tab management
- **Common patterns**: forms, dropdowns, infinite scroll, modals, pagination
- **Site-specific strategies**: LinkedIn, X/Twitter, Reddit, HackerNews, Amazon
- **Fallback strategies**: screenshot → coordinate click when element IDs fail
- **Error recovery**: stale IDs, blocked clicks, truncated pages

## Supported agents

Works with any agent that supports the skills format:

- Claude Code
- Cursor
- Windsurf
- Codex
- Amp
- Cline
- GitHub Copilot
- [and more](https://github.com/vercel-labs/skills)

## License

MIT
