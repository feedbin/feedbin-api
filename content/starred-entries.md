Starred Entries
===============

Starred entries deals only with entry_ids. After downloading the starred entry ids, you'll want to follow up with a call to

`GET /v2/entries.json?ids=4088,4089,4090,4091`

To actually retrieve the entries that have been starred. Please note, that you can only request up to 100 entries at a time.

Get Starred Entries
-------------------

- `GET /v2/starred_entries.json` will return an array of entry_ids

**Request**

```bash
curl --request GET \
--user "example@example.com:password" \
https://api.feedbin.com/v2/starred_entries.json
```

**Response**

```json
[4087,4088,4089,4090,4091,4092,4093,4094,4095,4096,4097]
```

**Status Codes**

- `200 OK` will be returned

Create Starred Entries
----------------------

- `POST /v2/starred_entries.json` will star the specified entry_ids

**Request**

```bash
curl --request POST \
--user "example@example.com:password" \
--header "Content-Type: application/json; charset=utf-8" \
--data-ascii '{"starred_entries": [4089, 4090, 4091]}' \
https://api.feedbin.com/v2/starred_entries.json
```

**Response**

```json
[4089,4090,4091]
```

The response will contain all of the entry_ids that were successfully starred. If any ids that were sent are not returned in the response it usually means the user no longer has access to the feed the entry belongs to.

**Status Codes**

- `200 OK` will be returned if the request is successful

**Note** There is a limit of 1,000 entry_ids per request


Delete Starred Entries (unstar)
-------------------------------

- `DELETE /v2/starred_entries.json` will remove unstar the specified entry_ids

**Request**

```bash
curl --request DELETE \
--user "example@example.com:password" \
--header "Content-Type: application/json; charset=utf-8" \
--data-ascii '{"starred_entries": [4089, 4090, 4091]}' \
https://api.feedbin.com/v2/starred_entries.json
```

**Response**

```json
[4089,4090,4091]
```

**Status Codes**

- `200 OK` will be returned if the request is successful

**Note** There is a limit of 1,000 entry_ids per request

The response will contain all of the entry_ids that were successfully unstarred. If any ids that were sent are not returned in the response it usually means the user no longer has access to the feed the entry belongs to.

**DELETE Alternative**

Some clients like Android don't easily allow a body with a DELETE request. For these cases there is an alternate endpoint that can be used with POST:

`POST /v2/starred_entries/delete.json`