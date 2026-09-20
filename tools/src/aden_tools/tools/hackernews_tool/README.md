# Hacker News Tool

Fetch top stories, search discussions, and look up items from Hacker News.
Uses the public [Firebase HN API](https://github.com/HackerNews/API) and
[Algolia HN Search API](https://hn.algolia.com/api). No API key required.

This is an unverified (community) tool — enable unverified tools to load it.

## Tools

| Tool | Description |
|------|-------------|
| `hn_get_top_stories` | Current top stories with optional score filter |
| `hn_search_stories` | Keyword search over HN stories |
| `hn_get_item` | Fetch one story or comment by numeric id |

## Parameters

### `hn_get_top_stories`

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | `int` | `10` | Number of stories to return (1–50) |
| `min_score` | `int` | `0` | Skip stories below this score |

### `hn_search_stories`

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | `str` | required | Search keywords |
| `limit` | `int` | `10` | Number of stories to return (1–50) |

### `hn_get_item`

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `item_id` | `int` | required | Hacker News item id |

## Usage Examples

```python
hn_get_top_stories(limit=5, min_score=100)
hn_search_stories(query="sqlite", limit=10)
hn_get_item(item_id=8863)
```

## Response Format

Top stories and search return:

```json
{
  "count": 1,
  "stories": [
    {
      "id": 8863,
      "title": "My YC app: Dropbox",
      "url": "http://www.getdropbox.com/u/2/screencast.html",
      "by": "dhouston",
      "score": 104,
      "time": 1175714200,
      "descendants": 71,
      "hn_url": "https://news.ycombinator.com/item?id=8863"
    }
  ]
}
```

Deleted, dead, and missing items return an error dict instead of raising:

```json
{"error": "Item 123 was deleted"}
```
