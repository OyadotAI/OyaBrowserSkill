# Oya Browser Skill

Teach any AI agent how to control a real browser through [Oya Browser](https://browser.oya.ai) MCP tools.

## Install

```bash
npx skills add OyadotAI/OyaBrowserSkill
```

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

## Requirements

- [Oya Browser](https://browser.oya.ai) installed and connected
- Oya Browser MCP server configured in your agent

## License

MIT
