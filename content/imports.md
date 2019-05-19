Imports
=======

The Imports API can be used to import OPML files and get the status of an import.

### `POST /v2/imports.json`

Create a new import. The POST body should be an XML string. Returns the import along with the status of each of the import_items. The `Content-Type` header must be set to `text/xml`.

```bash
curl --request POST --user "example@example.com:password" --header "Content-Type: text/xml" --data-binary "@/path/to/subscriptions.xml" https://api.feedbin.com/v2/imports.json
```

**Response**

```json
{
   "id": 6,
   "complete": false,
   "created_at": "2019-05-16T20:27:47.038Z",
   "import_items": [
     {
       "title": "Daring Fireball",
       "feed_url": "http://daringfireball.net/feeds/main",
       "status": "pending"
     }
   ]
}
```

The `id` can be used to get the status of the import at `/v2/imports/6.json`. 

### `GET /v2/imports.json`

Returns all imports for a user.

```bash
curl --request GET --user "example@example.com:password" https://api.feedbin.com/v2/imports.json
```

**Response**

```json
[
  {
    "id": 1,
    "complete": true,
    "created_at": "2019-05-16T19:58:59.214Z"
  },
  {
    "id": 2,
    "complete": false,
    "created_at": "2019-05-16T20:01:12.090Z"
  }
]
```


### `GET /v2/imports/1.json`

Returns the import along with the status of each of the import_items.

```bash
curl --request GET --user "example@example.com:password" https://api.feedbin.com/v2/imports/1.json
```

**Response**

```json
{
  "id": 4,
  "complete": true,
  "created_at": "2019-05-16T20:07:13.043Z",
  "import_items": [
    {
      "title": "Daring Fireball",
      "feed_url": "http://daringfireball.net/feeds/main",
      "status": "pending"
    },
    {
      "title": "inessential.com",
      "feed_url": "http://inessential.com/xml/rss.xml",
      "status": "complete"
    },
    {
      "title": "kottke.org",
      "feed_url": "http://feeds.kottke.org/main",
      "status": "failed"
    }
  ]
}
```

The possible values for `status` are:

- `pending` The feed is queued for import
- `complete` The feed has been successfully imported
- `failed` The import failed due to HTTP/invalid feed errors

