# Example prompts

Each prompt works in Claude, ChatGPT, Claude Code or Cursor once the connector
is added. Tool names in brackets are what the model is expected to call.

1. **Point and radius.** "Which security events happened within 5 km of
   41.0082, 28.9784 in the last 14 days? Give dates and sources."
   [`search_events` with `near_lat`, `near_lon`, `radius_km=5`, `date_from`]
2. **Country and category.** "List strikes in Germany in the last 30 days."
   [`list_categories`, then `search_events` with `countries=["DE"]`]
3. **Counts.** "How many protests were reported in Turkey each week this
   quarter?" [`event_stats` with `group_by=week`]
4. **One event.** "Open the first result and show every source link."
   [`get_event`]
5. **Address.** "What happened around Kadikoy, Istanbul last week?"
   [`search_events` with `address="Kadikoy Istanbul"`]
6. **Coverage.** "Which countries and dates can I search with this account?"
   [`get_coverage`]

Prompts the connector should not satisfy: creating, editing or deleting events;
predicting what will happen; anything about a named private person.
