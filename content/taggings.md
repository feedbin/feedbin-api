Taggings
========

Get Taggings
------------

 - `GET /v2/taggings.json` will return taggings.


```json
[
  {
    "id": 4,
    "feed_id": 1,
    "name": "Tech"
  },
  {
    "id": 5,
    "feed_id": 2,
    "name": "News"
  }
]
```

**Status Codes**

- `200 OK` will be returned

Get Tagging
-----------

- `GET /v2/taggings/4.json` will return the tagging with an id of `4`

```json
{
  "id": 4,
  "feed_id": 1,
  "name": "Tech"
}
```

**Status Codes**

- `200 OK` will be returned if found
- `403 Forbidden` will be returned if the user does not own this tagging

Create Tagging
--------------

- `POST /v2/taggings.json` will create a new tagging

**Request**

```json
{
  "feed_id": 1,
  "name": "Design"
}
```

| Parameter                        | Required |
| -------------------------------- | -------- |
| `feed_id: number`                | true     |
| `name: string`                   | true     |

**Status Codes**

- `201 Created` will be returned if tagging is successful, the `Location` header will have the URL to the newly created tagging
- `302 Found` will be returned if tagging exists, the `Location` header will have the URL to the tagging


Delete Tagging
--------------

`DELETE /v2/taggings/4.json` will delete the tagging with and id of `4`

**Status Codes**

- `204 No Content` will be returned if the request was successful
- `403 Forbidden` will be returned if the user does not own this tagging
