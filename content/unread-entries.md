Unread Entries
==============

Unread entries deals only with entry_ids. After downloading the unread entry ids, you'll want to follow up with a call to

`GET /v2/entries.json?ids=4088,4089,4090,4091`

To actually retrieve the unread entries. Please note, that you can only request up to 100 entries at a time.

Get Unread Entries
------------------

 - `GET /v2/unread_entries.json` will return an array of entry_ids


```json
[4087,4088,4089,4090,4091,4092,4093,4094,4095,4096,4097]
```

**Status Codes**

- `200 OK` will be returned

Create Unread Entries (mark as unread)
--------------------------------------

- `POST /v2/unread_entries.json` will mark the specified entry_ids as unread.

**Request**

```json
{
  "unread_entries": [4089, 4090, 4091]
}
```

**Response**

```json
[4089,4090,4091]
```

**Status Codes**

- `200 OK` will be returned if the request is successful

**Note** There is a limit of 1,000 entry_ids per request

The response will contain all of the entry_ids that were successfully marked as unread. If any ids that were sent are not returned in the response it usually means the user no longer has access to the feed the entry belongs to.

Delete Unread Entries (mark as read)
------------------------------------

- `DELETE /v2/unread_entries.json` will mark the specified entry_ids as read.

**Request**

```json
{
  "unread_entries": [4089, 4090, 4091]
}
```

**Status Codes**

- `200 OK` will be returned if the request is successful

**Note** There is a limit of 1,000 entry_ids per request

The response will contain all of the entry_ids that were successfully marked as read. If any ids that were sent are not returned in the response it usually means the user no longer has access to the feed the entry belongs to.

**DELETE Alternative**

Some clients like Android don't easily allow a body with a DELETE request. For these cases there is an alternate endpoint that can be used with POST:

`POST /v2/unread_entries/delete.json`
