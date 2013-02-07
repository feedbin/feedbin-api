Entry States
============

Entry states provide the users state information include read state and starred state.

Get Entry States
----------------

 - `GET /v1/entry_states.json` will return all entry states.


```json
[
  {
    "entry_id": 1,
    "read": true,
    "starred": true,
    "starred_updated_at": "2013-02-09T01:47:59Z",
    "read_updated_at": "2013-02-09T01:47:59Z"
  },
  {
    "entry_id": 1,
    "read": true,
    "starred": true,
    "starred_updated_at": "2013-02-09T01:47:59Z",
    "read_updated_at": "2013-02-09T01:47:59Z"
  },
  {
    entry_id: 3190,
    read: true,
    starred: false,
    starred_updated_at: null,
    read_updated_at: "2013-02-03T20:14:53Z"
  }
]
```

**Parameters**

 - `page: optional` `GET /v1/entry_states.json?page=2` will get page two of the entry states
 - `since: optional` `GET /v1/entry_states.json?since=2013-02-02T14:07:33Z` will get all entry states *updated* after 8601 timestamp.

Get Entry State
---------------

 - `GET /v1/entry_states/56.json` will return the entry state for entry_id `56`

```json
{
  entry_id: 56,
  read: true,
  starred: false,
  starred_updated_at: null,
  read_updated_at: "2013-02-03T20:15:03Z"
}
```

**Status Codes**

- `200 OK` will be returned if found
- `404 Not Found` will be returned if there is no saved entry state

Update/Create Entry States
--------------------------

- `POST v1/entry_states.json`

Entry states can be modified and created in bulk. Since multiple clients and the website might be updating the entry state, it is important to send *when* the state was changed. This prevents the case where an entry state is changed offline, and before it has a chance to sync, it is changed again. In this case the entry state update will be ignored. Clients should always save the time an action was performed, when it is performed rather than when it is sent.

If the timestamp that is sent is older than the timestamp that is saved, **the update will be ignored and does not trigger an error**. Instead it shows up in the succeeded array with the correct state.

**Request**

```json
{
  "entry_states": [
    {
      "entry_id": 1,
      "read": true,
      "starred": true,
      "starred_updated_at": "2013-02-09T01:47:59Z",
      "read_updated_at": "2013-02-09T01:47:59Z"
    },
    {
      "entry_id": 1,
      "read": true,
      "read": starred,
    }
  ]
}
```

**Parameters**
 - `entry_id required`
 - `starred_updated_at conditionally required` - an ISO 8601 timestamp. Required when attempting to change `read`
 - `read_updated_at conditionally required` - an ISO 8601 timestamp. Required when attempting to change `read`
 - `read` - boolean. True if read, false if unread
 - `starred` - boolean. True if starred, false if not starred

**Response**

```json
{
  "succeeded": [
    {
      "entry_id": 1,
      "read": true,
      "starred": true,
      "starred_updated_at": "2013-02-09T01:47:59Z",
      "read_updated_at": "2013-02-09T01:47:59Z"
    }
  ],
  "failed": [
    {
      "entry_id": 3,
      "errors": [
        {
          "field": "read_updated_at",
          "message": "must be present when updating read"
        },
        {
          "field": "starred_updated_at",
          "message": "must be present when updating starred"
        }
      ]
    }
  ]
}
```
