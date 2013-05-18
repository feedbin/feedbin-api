Starred Entries
===============

Starred entries deals only with entry_ids. After downloading the starred entry ids, you'll want to follow up with a call to

`GET /v2/entries.json?ids=4088,4089,4090,4091`

To actually retrieve the entries that have been starred. Please note, that you can only request up to 100 entries at a time.

Get Starred Entries
-------------------

 - `GET /v2/starred_entries.json` will return an array of entry_ids


```json
[4087,4088,4089,4090,4091,4092,4093,4094,4095,4096,4097]
```

**Status Codes**

- `200 OK` will be returned

Create Starred Entries
----------------------

- `POST /v2/starred_entries.json` will star the specified entry_ids

**Request**

```json
{
  "starred_entries": [4089, 4090, 4091]
}
```

**Status Codes**

- `200 OK` will be returned if the request is successful

**Note** There is a limit of 1,000 entry_ids per request

**Request**

`POST /v2/subscriptions.json`

```json
{
  "starred_entries": [4089, 4090, 4091]
}
```

**Response**

```json
[4089,4090,4091]
```

The response will contain all of the entry_ids that were successfully starred. If any ids that were sent are not returned in the response it usually means the user no longer has access to the feed the entry belongs to.

Delete Starred Entries (unstar)
-------------------------------

- `DELETE /v2/starred_entries.json` will remove unstar the specified entry_ids

**Request**

```json
{
  "starred_entries": [4089, 4090, 4091]
}
```

**Status Codes**

- `200 OK` will be returned if the request is successful

**Note** There is a limit of 1,000 entry_ids per request

The response will contain all of the entry_ids that were successfully unstarred. If any ids that were sent are not returned in the response it usually means the user no longer has access to the feed the entry belongs to.
