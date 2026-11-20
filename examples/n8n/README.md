# n8n workflows for AEGIS Risk Events

Import a file in n8n with **Workflows, Import from File**. Both use n8n's
built-in MCP nodes (n8n 1.x with the MCP Client nodes, tested on 2.48) and a
*Bearer Auth* credential holding your AEGIS API key
(free at https://console.int-tech.solutions/signup, 50 credits a month).

| File | What it does | AI model |
| --- | --- | --- |
| `daily-site-risk-digest.json` | Every morning, searches the last 24 hours around each of your sites and posts one digest per site to Slack | none: the MCP Client node calls `search_events` directly |
| `risk-events-chat-agent.json` | Chat with an AI agent that answers "what happened near X" with source links | yes (Anthropic node; swap for any chat model) |

Never put the key in the workflow JSON; keep it in the n8n credential.
