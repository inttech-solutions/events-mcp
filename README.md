# AEGIS Events MCP

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

Sign-up is closed for now. For a new account, contact
[info@int-tech.solutions](mailto:info@int-tech.solutions).

If you already have an account:

1. Sign in at [console.int-tech.solutions](https://console.int-tech.solutions).
2. Create an API key in the console, or connect an app with OAuth and choose
   "Continue with your AEGIS Events account".
3. Upgrade when you need more (see Limits).

## Connect

**Claude (claude.ai, Desktop)**: Settings, Connectors, Add custom connector,
URL `https://mcp.int-tech.solutions`. Sign in with your AEGIS Events account.

**ChatGPT**: Settings, Apps / Connectors, add a custom connector with the same
URL (developer mode may be required on your plan). Sign in with your AEGIS
Events account.

**Claude Code**:

```bash
claude mcp add --transport http aegis-events https://mcp.int-tech.solutions \
  --header "Authorization: Bearer aegis_live_..."
```

**Cursor** (`~/.cursor/mcp.json`) and other clients that read `mcpServers`:

```json
{
  "mcpServers": {
    "aegis-events": {
      "url": "https://mcp.int-tech.solutions",
      "headers": { "Authorization": "Bearer aegis_live_..." }
    }
  }
}
```

Never share a key. Keys are created and revoked in the console.

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

| Plan | Price (USD) | Requests | Max date window |
| --- | --- | --- | --- |
| Free | free | 50 a month | unlimited |
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
