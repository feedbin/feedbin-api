Feedbin API V2
==============

This is the official documentation for the Feedbin REST-style API.

V1 of the api has been deprecated, but the [documentation can still be accessed](v1/README.md). 

API Objects
-----------

- [Subscriptions](content/subscriptions.md)
- [Feeds](content/feeds.md)
- [Entries](content/entries.md)
- [Unread Entries](content/unread-entries.md)
- [Starred Entries](content/starred-entries.md)
- [Taggings](content/taggings.md)

Changes
-------
- 2013-05-20: Added `PATCH subscriptions.json` for editing feed titles to [Subscriptions](content/subscriptions.md#update-subscription)
- 2013-05-20: Added `per_page` paramter to [Entries](content/entries.md)

Upgrading from v1
-----------------

The `entry_states` object/concept has been removed from v2. Instead the functionality of `entry_states` has been split into [Unread Entries](content/unread-entries.md) and [Starred Entries](content/starred-entries.md). 

The only functionality changes you'll need to make are requests to any /v1/entry_states.json and any code that may reference the entry_state object.

The rest of the API remains the same as v1, so you'll want to find and replace v1 with v2.

Filtered entries.json vs. unread_entries.json
---------------------------------------------

Since `entries.json` supports filters for just getting unread items, why would you want to use `unread_entries.json`?

The issue with just relying on `entries.json?read=false` is things can get out of sync. Since `entries.json` is always sorted by the `created_at` timestamp for the entry, a user could subscribe to a feed today that had entries from yesterday or earlier.

In Feedbin, these entries would show up as unread, but if the API consumer was just using `entries.json?read=false&since=DATE` these entries would be missed.

Making Requests
---------------

The base URL for all requests is `https://api.feedbin.me/v2/` Only https is supported.

The Feedbin API uses HTTP Basic authentication

Using cURL you would make a request like: 

```shell
curl -u 'example@example.com:password' https://api.feedbin.me/v2/subscriptions.json
```

When creating or updating a record you must set `application/json; charset=utf-8` as the `Content-Type` header.

```shell
curl -u 'example@example.com:password' \
-H "Content-Type: application/json; charset=utf-8" \
-X POST -d '{"feed_url":"http://daringfireball.net"}' \
https://api.feedbin.me/v2/subscriptions.json
```

Without this header you'll wind up with a `415 Unsupported Media Type` response.

HTTP Caching, Use It
--------------------
For extra speed, please use HTTP Caching. `GET` request set ETag and a Last-Modified headers. 

```shell
curl -v -u 'example@example.com:password'  https://api.feedbin.me/v2/subscriptions/3.json
< ETag: "c7d001e87bda1f0d3745b6bd2811b055"
< Last-Modified: Sat, 02 Feb 2013 15:20:46 GMT
```

You can use these headers in subsequent requests like:

```shell
curl -v -u 'example@example.com:password' --header 'If-Modified-Since:Sat, 02 Feb 2013 15:20:46 GMT' --header 'If-None-Match:"c7d001e87bda1f0d3745b6bd2811b055"' https://api.feedbin.me/v2/subscriptions/3.json
< HTTP/1.1 304 Not Modified
```

Pagination
----------
Entries use pagination. Each page has a limit of 100 items. Paginated request will include a link header like:

```
Link: <https://api.feedbin.me/v2/feeds/1/entries.json?page=2>; rel="next", <https://api.feedbin.me/v2/feeds/1/entries.json?page=5>; rel="last"
```

The possible rel values are:

- `first` The URL of the first page of results.
- `prev` The URL of the previous page of results.
- `next` The URL of the next page of results.
- `last` The URL of the last page of results.

Dates
-----
The Feedbin API uses the [ISO 8601](http://www.w3.org/TR/NOTE-datetime) date format. All responses will include dates formatted to this spec and all requests should stick to it as well. The dates are as high resolution as possible to allow for rapid state changes. When using the `since` parameter it is best to include the date exactly as it was returned by the server when the last request was made. Rounding down to the nearest second will most likely cause duplicates.

The date should include complete date plus hours, minutes, seconds and timezone `YYYY-MM-DDThh:mm:ss.ssssssTZD` (eg `2013-02-19T07:33:38.449047-08:00` or in UTC `2013-02-19T15:33:38.449047Z`). All dates will be converted to UTC, so the timezone is very important.
