Feeds
=====

Get Feed
--------

- `GET /v2/feeds/1.json` will return the feed with an id of `1`

```json
{
  "id": 1,
  "title": "Ben Ubois",
  "feed_url": "http:\/\/feeds.feedburner.com\/benubois",
  "site_url": "http:\/\/benubois.com"
}
```

**Status Codes**

- `200 OK` will be returned if found
- `404 Not Found` will be returned if no feed is found