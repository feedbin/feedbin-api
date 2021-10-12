Subscriptions
=============

Get Subscriptions
-----------------

 - `GET /v2/subscriptions.json` will return all subscriptions.

```json
[
  {
    "id": 525,
    "created_at": "2013-03-12T11:30:25.209432Z",
    "feed_id": 47,
    "title": "Daring Fireball",
    "feed_url": "http://daringfireball.net/index.xml",
    "site_url": "http://daringfireball.net/"
  }
]
```

| Parameter     | Required | Example                                                                                                                          |
| ------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `since: date` | false    | `GET /v2/subscriptions.json?since=2013-03-08T09:44:20.449047Z` will get all subscriptions created after the iso 8601 timestamp.  |
| `mode: enum`  | false    | `GET /v2/subscriptions.json?mode=extended`  the only mode available is `extended`. This includes more metadata for the feed.     |


**Status Codes**

- `200 OK` will be returned if found
- `403 Forbidden` will be returned if the user does not own this subscription

Get Subscription
----------------

- `GET /v2/subscriptions/525.json` will return the feed with an id of `525`

```json
{
  "id": 525,
  "created_at": "2013-03-12T11:30:25.209432Z",
  "feed_id": 47,
  "title": "Daring Fireball",
  "feed_url": "http://daringfireball.net/index.xml",
  "site_url": "http://daringfireball.net/"
}
```

#### About `extended` Mode

The `extended` mode includes a additional meta-data for subscriptions. Currently this includes a `json_feed` key with all of the additional metadata that a [JSON Feed offers](https://jsonfeed.org/version/1).

```json
[
  {
    "id" : 1,
    "feed_id" : 1,
    "site_url" : "https://micro.blog/",
    "title" : "Micro.blog - manton timeline",
    "feed_url" : "https://micro.blog/feeds/manton.json",
    "created_at" : "2019-05-23T23:49:14.487938Z",
    "json_feed" : {
      "favicon" : "https://micro.blog/images/icons/favicon_32.png",
      "feed_url" : "https://micro.blog/feeds/manton.json",
      "icon" : "https://micro.blog/images/icons/favicon_256.png",
      "version" : "https://jsonfeed.org/version/1",
      "home_page_url" : "https://micro.blog/",
      "title" : "Micro.blog - manton timeline"
    }
  }
]
```

**Status Codes**

- `200 OK` will be returned if found
- `403 Forbidden` will be returned if the user does not own this subscription

Create Subscription
-------------------

- `POST /v2/subscriptions.json` will create a new subscription to the specified `feed_url`

**Request**

```json
{
  "feed_url": "http://daringfireball.net/index.xml"
}
```

| Parameter          | Required | Example                                                                                                                                    |
| ------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `feed_url: string` | true     | can be the fully qualified url to the feed like `http://daringfireball.net/index.xml`, or the url to the website like `daringfireball.net` |


**Status Codes**

- `201 Created` will be returned if subscription is successful, the `Location` header will have the URL to the newly created subscription
- `302 Found` will be returned if subscription exists, the `Location` header will have the URL to the newly created subscription
- `404 Not Found` will be returned if no feed is found at the `feed_url`
- `300 Multiple Choices` will be returned if multiple feeds are found at the `feed_url` 

If `201` or `302` are returned, the response will be the same as **Get Subscription**:

**Request**

```json
{
  "feed_url": "http://daringfireball.net/"
}
```

**Response**

```json
{
    "id": 4105850,
    "created_at": "2017-10-28T14:30:39.324314Z",
    "feed_id": 838741,
    "title": "Daring Fireball",
    "feed_url": "https://daringfireball.net/feeds/main",
    "site_url": "https://daringfireball.net/"
}
```

If a `300 Multiple Choices` is returned, it means the requested site exposes more than one feed. In this case the response will let you know what the options are. For example:

**Request**

`POST /v2/subscriptions.json`

```json
{
  "feed_url": "https://blog.github.com"
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

`DELETE /v2/subscriptions/3.json` will delete the subscription with an id of `3`

**Status Codes**

- `204 No Content` will be returned if the request was successful
- `403 Forbidden` will be returned if the user does not own this subscription

Update Subscription
-------------------

Updating a subscrition can be used to set a custom title for a feed.

`PATCH /v2/subscriptions/525.json` will update the subscription with an id of `525`


**Request**

```json
{
  "title": "Custom Title"
}
```

**Response**

```json
{
  "id": 525,
  "created_at": "2013-03-12T11:30:25.209432Z",
  "feed_id": 47,
  "title": "Custom Title",
  "feed_url": "http://daringfireball.net/index.xml",
  "site_url": "http://daringfireball.net/"
}
```

**Status Codes**

- `200 OK` will be returned if the request was successful
- `403 Forbidden` will be returned if the user does not own this subscription

**PATCH Alternative**

Some proxies block or filter PATCH requests. A POST alternative is available for these cases:

`POST /v2/subscriptions/525/update.json` will update the subscription with an id of `525`

Thanks to [Oliver Fürniß](http://curioustimes.de/) for pointing this out.
