# Tavily Claude Code Plugin

Build AI applications with real-time web data using Tavily's search, extract, crawl, and research APIs.

## Prerequisites

**Tavily API Key Required** - Get your key at https://tavily.com

Add to your Claude Code settings (`~/.claude/settings.json`):

```json
{
  "env": {
    "TAVILY_API_KEY": "tvly-your-api-key-here"
  }
}
```

## Installation

### Option 1: Via Marketplace (Recommended)

```bash
# Add the Tavily marketplace
claude plugin marketplace add tavily-ai/tavily-cookbook

# Install the plugin
claude plugin install tavily
```

### Option 2: Direct Install

```bash
claude plugin install github:tavily-ai/tavily-cookbook/tavily
```

## Skills

The plugin includes three agent skills that Claude can use automatically:

| Skill | Description |
|-------|-------------|
| **tavily-api** | Reference documentation for Tavily's search, extract, crawl, and research APIs. Includes best practices for agentic workflows. |
| **research** | CLI tool for AI-synthesized research with citations. Supports structured JSON output. |
| **crawl-url** | Website crawler that saves pages as local markdown files for offline analysis. |

## Links

- [Tavily Documentation](https://docs.tavily.com)
- [Tavily Cookbook](https://github.com/tavily-ai/tavily-cookbook)
- [Get API Key](https://tavily.com)

## License

MIT
