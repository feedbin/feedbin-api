Actions
=======

Actions run automatically on new entries that match a search query, for example to mark matching entries as read or to star them. They are the same Actions that can be managed at Settings → Actions.

Action Object
-------------

```json
{
  "id": 1,
  "title": "Mute sponsored posts",
  "action_type": "standard",
  "actions": [
    "mark_read"
  ],
  "query": "sponsored",
  "feed_ids": [
    42
  ],
  "tag_ids": []
}
```

| Field                   | Description |
| ----------------------- | ----------- |
| `id: number`            | The action's id |
| `title: string`         | The action's title |
| `action_type: string`   | One of `standard`, `notifier` or `mute` |
| `actions: array`        | What to do with matching entries: `mark_read`, `star`, `send_push_notification`, `send_ios_notification` |
| `query: string`         | A search query, using the same syntax as Feedbin search |
| `feed_ids: array`       | The feeds the action applies to |
| `tag_ids: array`        | The tags the action applies to. Feeds with these tags are included |

When both `feed_ids` and `tag_ids` are empty, the action applies to all feeds.

Get Actions
-----------

- `GET /v2/actions.json` will return all actions

| Parameter              | Required | Example |
| ---------------------- | -------- | ------- |
| `action_type: string`  | false    | `GET /v2/actions.json?action_type=notifier` will only return actions of this type |

**Status Codes**

- `200 OK` will be returned

Create Action
-------------

- `POST /v2/actions.json` will create a new action

This request requires the `Content-Type: application/json; charset=utf-8` header.

**Request**

```json
{
  "action_params": {
    "query": "sponsored",
    "actions": ["mark_read"],
    "feed_ids": [],
    "tag_ids": []
  }
}
```

| Parameter              | Required |
| ---------------------- | -------- |
| `query: string`        | false    |
| `action_type: string`  | false    |
| `actions: array`       | false    |
| `feed_ids: array`      | false    |
| `tag_ids: array`       | false    |

The response is the new action object.

**Status Codes**

- `200 OK` will be returned
- `415 Unsupported Media Type` will be returned if the `Content-Type` header is missing

Update Action
-------------

- `PATCH /v2/actions/1.json` will update the action with an id of `1`

**Request**

```json
{
  "action_params": {
    "query": "sponsored OR giveaway",
    "feed_ids": [42],
    "actions": ["mark_read"]
  }
}
```

The response is the updated action object.

**Status Codes**

- `200 OK` will be returned if the request was successful
- `400 Bad Request` will be returned if the action could not be saved
- `404 Not Found` will be returned if the user does not own this action

Get Action Results
------------------

- `GET /v2/actions/1/results.json` will return entries that currently match the action

| Parameter         | Required | Example |
| ----------------- | -------- | ------- |
| `read: bool`      | false    | `GET /v2/actions/1/results.json?read=false` will only return unread matching entries |

The response is an array of [entry objects](entries.md).

**Status Codes**

- `200 OK` will be returned
- `404 Not Found` will be returned if the user does not own this action

Deleting Actions
----------------

Actions can't be deleted through the API. Delete them at Settings → Actions.
