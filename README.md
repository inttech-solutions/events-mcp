# AEGIS Risk Events MCP

A hosted, read-only MCP server for security events extracted from the news:
protests, strikes, crime, terrorism, accidents, natural hazards and political
unrest. Each event is one English sentence with its date, place, category,
importance and source links. Search by country, address, a point plus radius
(`near_lat`, `near_lon`, `radius_km`), category and date.

This repository holds documentation and registry metadata only. The server is
hosted by [INT-TECH](https://www.int-tech.solutions) at:

```
https://mcp.int-tech.solutions
```

Transport: streamable HTTP. Sign-in: OAuth (account sign-in in the console) or
an API key.

## Get access

Create a free account at [console.int-tech.solutions](https://console.int-tech.solutions/signup)
with email or Google. You get 50 credits a month, no card needed.

1. Connect an app with OAuth (choose "Sign in to the console"), or create an API key in the console.
2. Upgrade when you need more (see Limits). Pro and Team open when card payments go live.

## Connect

**Claude (claude.ai, Desktop)**: Settings, Connectors, Add custom connector,
URL `https://mcp.int-tech.solutions`. Sign in with your AEGIS account.

**ChatGPT**: Settings, Apps / Connectors, add a custom connector with the same
URL (developer mode may be required on your plan). Sign in with your AEGIS account.

**Claude Code**: this repository ships a project `.mcp.json`, so inside a clone
the server is already configured. Or add it yourself and sign in with OAuth
through `/mcp`:

```bash
claude mcp add --transport http aegis-risk-events https://mcp.int-tech.solutions
```

With an API key instead of OAuth, keep the key in an environment variable, not in a file:

```bash
claude mcp add --transport http aegis-risk-events https://mcp.int-tech.solutions \
  --header "Authorization: Bearer $AEGIS_API_KEY"
```

**Cursor**: the project file `.cursor/mcp.json` in this repository is enough
(Cursor signs you in with OAuth). For all projects, put the same block in
`~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "aegis-risk-events": {
      "url": "https://mcp.int-tech.solutions"
    }
  }
}
```

With an API key, read it from the environment so it never lands in a file:

```json
{
  "mcpServers": {
    "aegis-risk-events": {
      "url": "https://mcp.int-tech.solutions",
      "headers": { "Authorization": "Bearer ${env:AEGIS_API_KEY}" }
    }
  }
}
```

Do not commit a key. If one leaks, revoke it in the console.

**Cline**: add `{"type": "streamableHttp", "url": "https://mcp.int-tech.solutions"}`
under `mcpServers` in `cline_mcp_settings.json`. Agents can follow
[llms-install.md](llms-install.md).

**n8n**: use the built-in MCP Client nodes with a Bearer Auth credential. Ready
workflows (daily digest for your sites, chat agent) are in [examples/n8n](examples/n8n).


## Tools

All tools are read-only.

| Tool | What it does |
| --- | --- |
| `search_events` | Find events by meaning (`query`), exact names (`keywords`) and filters (countries, address, point + `radius_km` up to 50 km, categories, dates); pages with `next_cursor` |
| `get_event` | Full record of one event: descriptions, every source URL, actors |
| `event_stats` | Event counts by day, week, month, category or country |
| `list_categories` | The category tree and the slugs `categories` accepts |
| `get_coverage` | Countries and dates your account can see, and your plan's limits |

Without dates, the last 30 days are searched. Count with `event_stats`, not by
paging through `search_events`. More prompts: [examples/prompts.md](examples/prompts.md).

## Limits

| Plan | Price (USD) | Credits | Max date window |
| --- | --- | --- | --- |
| Free | free | 50 a month | 90 days |
| Pro | $19 a month or $180 a year | 500 a month | 365 days |
| Team | $79 a month or $780 a year | 3,000 a month | 730 days |
| Enterprise | contact us | custom | custom |

The quota belongs to the workspace and is shared by its keys and connected
apps. Plan details in the console are authoritative.

## Links

- Console and pricing: https://console.int-tech.solutions
- Developer docs: https://console.int-tech.solutions/docs
- Terms: https://console.int-tech.solutions/legal/terms
- Privacy: https://console.int-tech.solutions/legal/privacy
- Support: info@int-tech.solutions (also https://mcp.int-tech.solutions/support)
