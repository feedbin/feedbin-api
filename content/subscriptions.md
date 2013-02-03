Subscriptions
=============

Get Subscriptions
-----------------

 - `GET /api/v1/subscriptions.json` will return all subscriptions.

```json
[
  {
    "id":3,
    "created_at":"2013-02-02T15:20:46Z",
    "title":"Daring Fireball",
    "feed_url":"http://daringfireball.net/index.xml",
    "site_url":"http://daringfireball.net"
  }
]
```

**Parameters**

 - `since: optional` `GET /api/v1/subscriptions.json?since=2013-02-02T14:07:33Z` will get all subscriptions created after the iso 8601 timestamp.

**Status Codes**

- `200 OK` will be returned if found
- `403 Forbidden` will be returned if the user does not own this subscription
 
 
Get Subscription
----------------

- `GET /api/v1/subscriptions/3.json` will return the feed with an id of `3`

```json
{
  "id":3,
  "created_at":"2013-02-02T15:20:46Z",
  "title":"Daring Fireball",
  "feed_url":"http://daringfireball.net/index.xml",
  "site_url":"http://daringfireball.net"
}
```

**Status Codes**

- `200 OK` will be returned if found
- `403 Forbidden` will be returned if the user does not own this subscription

Create Subscription
-------------------

- `POST /api/v1/subscriptions.json` will create a new subscription to the specified `feed_url`

```json
{
  "feed_url": "http://daringfireball.net/index.xml",
}
```

Feed url can be the fully qualified url to the feed like `http://daringfireball.net/index.xml`, or the url to the website like `daringfireball.net`

**Status Codes**

- `201 Created` will be returned if subscription is successful, the `Location` header will have the URL to the newly created subscription
- `302 Found` will be returned if subscription exists, the `Location` header will have the URL to the newly created subscription
- `404 Not Found` will be returned if no feed is found at the `feed_url`
- `300 Multiple Choices` will be returned if multiple feeds are found at the `feed_url` for example: 

**Request**

`POST /api/v1/subscriptions.json`

```json
{
  "feed_url": "https://blog.github.com",
}
```

**Response**

```json
[
  {
    "feed_url": "https://github.com/blog.atom",
    "title": "The GitHub Blog"
  },
  {
    "feed_url": "https://github.com/blog/broadcasts.atom",
    "title": "The GitHub Blog (Broadcasts)"
  }
]
```

Delete Subscription
-------------------

`DELETE /api/v1/subscriptions/3.json` will delete the subscription with and id of `3`

**Status Codes**

- `204 No Content` will be returned if the request was successful
- `403 Forbidden` will be returned if the user does not own this subscription