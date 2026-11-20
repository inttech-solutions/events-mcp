# Installing AEGIS Risk Events (for AI agents)

AEGIS Risk Events is a hosted, remote MCP server. There is nothing to clone,
build or run locally: add the URL below to the MCP client's settings.

- Endpoint: `https://mcp.int-tech.solutions`
- Transport: streamable HTTP
- Auth: OAuth (the client opens a browser sign-in on first use) or an API key
  sent as `Authorization: Bearer aegis_live_...`
- Account: free at https://console.int-tech.solutions/signup (50 credits a month, no card)

## Cline

Add this to `cline_mcp_settings.json` (Cline: MCP Servers, Configure, "Configure MCP Servers"):

```json
{
  "mcpServers": {
    "aegis-risk-events": {
      "type": "streamableHttp",
      "url": "https://mcp.int-tech.solutions"
    }
  }
}
```

Cline signs the user in with OAuth when the server is first used. If the user
prefers an API key, ask them to create one in the console and add it as a
header. Do not write the key into a file that is committed to git:

```json
{
  "mcpServers": {
    "aegis-risk-events": {
      "type": "streamableHttp",
      "url": "https://mcp.int-tech.solutions",
      "headers": { "Authorization": "Bearer <AEGIS_API_KEY>" }
    }
  }
}
```

## Check that it works

Call `get_coverage` (free). It returns the countries and dates available.
Then try `search_events` with `near_lat` 41.0082, `near_lon` 28.9784 and
`radius_km` 5 (Istanbul) for the last 7 days.

## Tools

| Tool | Credits |
| --- | --- |
| `search_events`: events by `query`, `keywords`, country, address, point + radius, category, date | 1 |
| `get_event`: full record of one event with every source link | 1 |
| `event_stats`: counts by day, week, month, category or country | 1 |
| `list_categories`: category slugs that `categories` accepts | free |
| `get_coverage`: countries, dates and limits | free |

An empty result does not mean an area was calm: coverage is denser in some
countries (Turkey and Europe) than others.
