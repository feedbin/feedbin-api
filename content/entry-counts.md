Entry Counts
============

Get Post Frequency
------------------

- `GET /v2/entry_counts/post_frequency.json` will return the number of new entries per day across all of the user's subscriptions, oldest day first

```json
[345, 362, 186, 168, 347, 343, 20]
```

| Parameter      | Required | Example |
| -------------- | -------- | ------- |
| `days: number` | false    | `GET /v2/entry_counts/post_frequency.json?days=30` will cover the last 30 days. The default is 6, which returns 7 values: the last 6 days and today |

**Status Codes**

- `200 OK` will be returned
