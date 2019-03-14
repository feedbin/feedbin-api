Icons
=====

### `GET /v2/icons.json`

Returns the feed icons (favicons) for all the feeds a user is subscribed to. Icons are resized to a max resolution of 32x32. If an icon is missing it means Feedbin was unable to find it.

```bash
curl --request GET --user "example@example.com:password" https://api.feedbin.com/v2/icons.json
```

**Response**

```json
[
  {
      "host": "m.signalvnoise.com",
      "url": "https://favicons.feedbinusercontent.com/27a/27a62660e820f80421e1e57551b070e6e42e52d4.png"
  },
  {
      "host": "github.blog",
      "url": "https://favicons.feedbinusercontent.com/19a/19ae11001100ad1497fba45580a546b022c2a8d3.png"
  }
]
```
