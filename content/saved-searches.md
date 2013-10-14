Saved Searches
==============

Get Saved Searches
------------------

 - `GET /v2/saved_searches.json` will return all saved_searches.

```json
[
  {
    "id": 1,
    "name": "JavaScript",
    "query": "javascript is:unread"
  }
]
```

**Status Codes**

- `200 OK` will be returned

Get Saved Search
----------------

- `GET /v2/saved_searches/1.json` will return the entry_ids of the matching entries

```json
[
	2058,
	1,
	1525,
	1025,
	410,
	432
]
```

By default an array of entry ids is returned in the correct order. The theory is that you will already have some or all of the entries and the ones that you don't yet have can be picked up using `GET /v2/entries.json?ids=1,2,3`.

| Parameter               | Required | Example                                                                                                                                    |
| ----------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `include_entries: bool` | false    | `GET /v2/saved_searches/1.json?include_entries=true` will return entry objects instead of an array of entry_ids                            |
| `page: number`          | false    | `GET /v2/saved_searches.json?page=2`  will get page two of the search results                                                              |

**Status Codes**

- `200 OK` will be returned if found
- `403 Forbidden` will be returned if the user does not own this saved search

Create Saved Search
-------------------

- `POST /v2/saved_searches.json` will create a new saved search with the specified parameters

**Request**

```json
{
  "name": "JavaScript",
  "query": "javascript is:unread"
}
```

| Parameter       | Required |
| --------------- | -------- |
| `name: string`  | true     |
| `query: string` | true     |


**Status Codes**

- `201 Created` will be returned if creating the saved search is successful, the `Location` header will have the URL to the newly created saved search

Delete Saved Search
-------------------

`DELETE /v2/saved_searches/1.json` will delete the saved search with and id of `1`

**Status Codes**

- `204 No Content` will be returned if the request was successful
- `403 Forbidden` will be returned if the user does not own this saved search

Update Saved Search
-------------------

Updating a saved search can be used to set a custom title for a feed.

`PATCH /v2/saved_searches/1.json` will update the saved search with and id of `1`


**Request**

```json
{
  "name": "Unread JavaScript"
}
```

**Response**

```json
{
  "id": 1,
  "name": "Unread JavaScript",
  "query": "javascript is:unread"
}
```

**Status Codes**

- `200 OK` will be returned if the request was successful
- `403 Forbidden` will be returned if the user does not own this saved search

**PATCH Alternative**

Some proxies block or filter PATCH requests. A POST alternative is available for these cases:

`POST /v2/saved_searches/1/update.json` will update the saved search with and id of `1`
