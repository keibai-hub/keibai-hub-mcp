# 不動産競売 構造化データハブ — Japan real-estate auctions MCP server

[![Smithery](https://img.shields.io/badge/smithery-listed-blue)](https://smithery.ai/server/keibai-hub)

Japanese court-run real-estate auction registry (BIT, bit.courts.go.jp) re-published as a structured Remote MCP server.

- **~1,480** active auctions
- **46** prefectures
- **110+** district courts and branches
- Updated **twice daily** (06:07 / 18:07 JST)

## Connect

Remote MCP endpoint (Streamable HTTP):

```
https://keibai-hub.com/mcp-auctions
```

### Claude Desktop / Cursor / Cline

Add to your `mcp_servers` config:

```json
{
  "keibai-hub": {
    "url": "https://keibai-hub.com/mcp-auctions"
  }
}
```

### Smithery one-click

[![Add to Smithery](https://smithery.ai/badge/keibai-hub.svg)](https://smithery.ai/server/keibai-hub)

## Tools (5)

| Tool | Description |
|---|---|
| `search_auctions` | Search by keyword (Japanese FTS over title/address) / prefecture / court_code / property_type / price range / bid_period_only |
| `get_auction_detail` | Fetch one auction by case_id (e.g. `bit_00000078922`) — returns case_number, court, price, bid period, photos, etc. |
| `list_upcoming_sales` | List auctions whose opening_date falls within the next N days (default 14, max 90) |
| `get_court_directory` | Look up a Japanese district court (本庁 or 支部) by code |
| `find_practitioner_for_auction` | Returns 司法書士 / 弁護士 / 不動産鑑定士 / 土地家屋調査士 federation directories for a given auction stage (post_acquisition / pre_bid / eviction / boundary_dispute) |

## Data sources & license

- Source: BIT (https://www.bit.courts.go.jp/, 最高裁判所) under 民事執行法 64 条 5 項 公示原則
- Structuring layer license: **CC BY 4.0** — attribute the canonical `_canonical` URL of each record
- This service is **information-only** and does not act as a paid intermediary
- BIT URLs are session-bound; use the `bit_lookup_hint` field (case_number) to search BIT manually

## REST API (no MCP)

If you prefer plain HTTP without MCP:

- `GET https://keibai-hub.com/api/auctions/search?prefecture=東京都&limit=20`
- `GET https://keibai-hub.com/api/auctions/{case_id}`
- `GET https://keibai-hub.com/api/auctions/{case_id}.md` (Markdown variant, token-efficient)
- `GET https://keibai-hub.com/api/auctions/coverage`
- `GET https://keibai-hub.com/api/auctions/upcoming?days_ahead=14`
- `GET https://keibai-hub.com/.well-known/coverage-auctions.json`
- `GET https://keibai-hub.com/llms.txt`

## Contact

Issues and feature requests via GitHub issues.

## License

MIT (this repository's metadata only — the auction data carries CC BY 4.0).
