Suggested Feeds
===============

Feedbin keeps a curated list of feeds, grouped into categories, that its apps offer to new users.

Get Suggested Categories
------------------------

- `GET /v2/suggested_categories.json` will return all categories

```json
[
  {
    "id": 2,
    "name": "Tech",
    "icon_url": "https://assets.feedbin.com/assets/suggested-categories/category-2.png"
  }
]
```

**Status Codes**

- `200 OK` will be returned

Get Suggested Feeds
-------------------

- `GET /v2/suggested_feeds.json` will return all suggested feeds

```json
[
  {
    "id": 1,
    "feed_id": 1713,
    "suggested_category_id": 8,
    "title": "The Verge",
    "host": "www.theverge.com"
  }
]
```

`suggested_category_id` matches the `id` of a suggested category, and `feed_id` matches the `feed_id` of a [subscription](subscriptions.md).

**Status Codes**

- `200 OK` will be returned

Subscribe to a Suggested Feed
-----------------------------

- `POST /v2/suggested_feeds/1/subscribe.json` will subscribe the user to the suggested feed with an id of `1`

**Status Codes**

- `201 Created` will be returned if the user is subscribed
- `400 Bad Request` will be returned if the subscription could not be created

Unsubscribe from a Suggested Feed
---------------------------------

- `DELETE /v2/suggested_feeds/1/unsubscribe.json` will unsubscribe the user from the suggested feed with an id of `1`

**Status Codes**

- `204 No Content` will be returned if the user is no longer subscribed
- `400 Bad Request` will be returned if the subscription could not be removed
