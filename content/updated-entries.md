Updated Entries
===============

Updated entries are entries that have been modified after they were originally published.

Feedbin stores both the original version of an entry and the latest version.

The updated entry API can give you a list of entry ids that have been updated. After downloading the unread entry ids, you can get the entries themselves including the original content.

`GET /v2/entries.json?include_original=true&ids=4088,4089,4090,4091`

On the web [Feedbin gives the user an option to show a diff of the original and the latest](http://blog.feedbin.com/2014/12/16/never-miss-an-update-with-the-new-updated-section/) which highlights what has changed.

Get Updated Entries
-------------------

 - `GET /v2/updated_entries.json` will return an array of entry_ids


```json
[4087,4088,4089,4090,4091,4092,4093,4094,4095,4096,4097]
```

**Status Codes**

- `200 OK` will be returned

**Note** The order of IDs is how

Delete Updated Entries (mark as read)
-------------------------------------

- `DELETE /v2/updated_entries.json` will mark the specified entry_ids as read.

**Request**

```json
{
  "updated_entries": [4089, 4090, 4091]
}
```

**Status Codes**

- `200 OK` will be returned if the request is successful

The response will contain all of the entry_ids that were successfully deleted.

**DELETE Alternative**

Some clients like Android don't easily allow a body with a DELETE request. For these cases there is an alternate endpoint that can be used with POST:

`POST /v2/updated_entries/delete.json`
