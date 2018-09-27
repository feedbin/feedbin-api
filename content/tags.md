Tags
====

### `POST /v2/tags.json`

Rename a tag.

```bash
curl --request POST \
--user "example@example.com:password" \
--header "Content-Type: application/json; charset=utf-8" \
--data-ascii '{"old_name": "Old Name", "new_name": "New Name"}' \
https://api.feedbin.com/v2/tags.json
```

**Request**

```json
{
  "old_name": "Old Name",
  "new_name": "New Name"
}
```

**Response**

Returns the new array of [taggings](taggings.md) after the rename.

```json
[
  {
    "id": 4,
    "feed_id": 1,
    "name": "New Name"
  }
]
```

### `DELETE /v2/tags.json`

Delete a tag.

```bash
curl --request DELETE \
--user "example@example.com:password" \
--header "Content-Type: application/json; charset=utf-8" \
--data-ascii '{"name": "Tag Name"}' \
https://api.feedbin.com/v2/tags.json
```

**Request**

```json
{
  "name": "Tag Name"
}
```

**Response**

Returns the new array of [taggings](taggings.md) after the delete.

```json
[
  {
    "id": 4,
    "feed_id": 1,
    "name": "Other Tag"
  }
]
```
