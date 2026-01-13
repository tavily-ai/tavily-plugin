---
name: deal-hunt
description: "Find the best current deals/coupons for a specific product. Searches web for deals and returns raw results for analysis."
---

# Deal Hunt

Search for deals on any product. Returns raw Tavily search results - Claude analyzes them to find the best prices.

## Prerequisites

**Tavily API Key Required** - Get your key at https://tavily.com

Add to `~/.claude/settings.json`:
```json
{
  "env": {
    "TAVILY_API_KEY": "tvly-your-api-key-here"
  }
}
```

## Usage

```bash
# Search entire web (default - no domain filter)
python scripts/deal_hunt.py "Dyson V15"

# Multi-query search (max 3, runs in parallel, deduplicates results)
python scripts/deal_hunt.py "AirPods Pro" --queries "AirPods Pro deal,AirPods Pro coupon,AirPods Pro discount"

# Limit to specific sites
python scripts/deal_hunt.py "MacBook Air" --domains amazon.com,walmart.com,bestbuy.com

# Custom single query
python scripts/deal_hunt.py "Nintendo Switch" --query "Nintendo Switch OLED bundle deal"

# Fresh deals only
python scripts/deal_hunt.py "PS5" --time-range day
```

## CLI Parameters

| Option | Short | Default | Description |
|--------|-------|---------|-------------|
| `product` | - | Required | Product name |
| `--query` | `-q` | `{product} deal price` | Single custom search query |
| `--queries` | | None | Comma-separated queries (max 3), runs in parallel with dedup |
| `--domains` | `-d` | None (search all) | Optionally limit to specific domains |
| `--max-results` | `-n` | 10 | Number of results per query |
| `--time-range` | `-t` | week | day, week, month, year, none |
| `--search-depth` | `-s` | advanced | basic, advanced, fast, ultrafast |

## Output

Returns JSON with results:

```json
{
  "meta": {
    "product": "AirPods Pro",
    "queries": ["AirPods Pro deal", "AirPods Pro coupon"],
    "domains": null,
    "time_range": "week",
    "search_time": "2026-01-13T...",
    "total_results": 15
  },
  "results": [
    {
      "title": "...",
      "url": "https://...",
      "content": "...",
      "score": 0.95
    }
  ]
}
```

When using `--queries`, results are deduplicated by URL (highest score kept, content merged).

Claude analyzes the results to extract prices, compare deals, and recommend the best option.
