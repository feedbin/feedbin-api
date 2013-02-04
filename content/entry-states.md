Entry States
============

Entry states provide the users state information include read state and starred state.

Get Entry States
----------------

 - `GET /api/v1/entry_states.json` will return all entry states.


```json
[
  {
    entry_id: 56,
    read: true,
    starred: false,
    starred_updated_at: null,
    read_updated_at: "2013-02-03T20:15:03Z"
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

 - `page: optional` `GET /api/v1/entry_states.json?page=2` will get page two of the entry states
 - `since: optional` `GET /api/v1/entry_states.json?since=2013-02-02T14:07:33Z` will get all entry states *updated* after 8601 timestamp.

Get Entry State
---------------

 - `GET /api/v1/entry_states/56.json` will return the entry state for entry_id `56`

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
