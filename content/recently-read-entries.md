Recently Read Entries
=====================

Recently read entries are a history of what the user has recently read.

Recently read entries are created if a user is on a post for 10 seconds on Feedbin, but you can use any metric makes sense for determining if an entry should end up here.

Get Recently Read Entries
-------------------------

 - `GET /v2/recently_read_entries.json` will return an array of entry_ids


```json
[4087,4088,4089,4090,4091,4092,4093,4094,4095,4096,4097]
```

**Status Codes**

- `200 OK` will be returned


**Note** The order of IDs is the order these should be displayed in


Create Recently Read Entries
----------------------------

- `POST /v2/recently_read_entries.json` will create records for the specified entry_ids.

**Request**

```json
{
  "recently_read_entries": [4089, 4090, 4091]
}
```

**Response**

```json
[4089,4090,4091]
```

**Status Codes**

- `200 OK` will be returned if the request is successful

The response will contain the entry_ids of the recently read records that were created.