Feedbin API V2
==============

This is the official documentation for the Feedbin REST-style API.

API Objects
-----------

- [Authentication](content/authentication.md)
- [Subscriptions](content/subscriptions.md)
- [Entries](content/entries.md)
- [Unread Entries](content/unread-entries.md)
- [Starred Entries](content/starred-entries.md)
- [Taggings](content/taggings.md)
- [Tags](content/tags.md)
- [Saved Searches](content/saved-searches.md)
- [Recently Read Entries](content/recently-read-entries.md)
- [Updated Entries](content/updated-entries.md)
- [Icons](content/icons.md)
- [Imports](content/imports.md)
- [Pages](content/pages.md)

Tech Notes
----------

- [Extracting Full Content](content/extract-full-content.md)
- [Supporting Twitter](content/supporting-twitter.md)

Changes
-------
- 2019-12-27: Added [Pages API](content/pages.md)
- 2019-05-17: Added [Imports API](content/imports.md)
- 2019-03-13: Added [Icons API](content/icons.md)
- 2015-01-22: Added [Updated Entries API](content/updated-entries.md)
- 2015-01-22: Added [Recently Read Entries API](content/recently-read-entries.md)
- 2013-10-14: Added [Saved Search API](content/saved-searches.md)
- 2013-05-20: Added `PATCH subscriptions.json` for editing feed titles to [Subscriptions](content/subscriptions.md#update-subscription)
- 2013-05-20: Added `per_page` paramter to [Entries](content/entries.md)

Making Requests
---------------

The base URL for all requests is `https://api.feedbin.com/v2/` Only https is supported.

The Feedbin API uses HTTP Basic authentication

Using cURL you would make a request like:

```shell
curl -u 'example@example.com:password' https://api.feedbin.com/v2/subscriptions.json
```

When creating or updating a record you must set `application/json; charset=utf-8` as the `Content-Type` header.

```shell
curl -u 'example@example.com:password' \
-H "Content-Type: application/json; charset=utf-8" \
-X POST -d '{"feed_url":"http://daringfireball.net"}' \
https://api.feedbin.com/v2/subscriptions.json
```

Without this header you'll wind up with a `415 Unsupported Media Type` response.

HTTP Caching, Use It
--------------------
For extra speed, please use HTTP Caching. `GET` request set ETag and a Last-Modified headers.

```shell
curl -v -u 'example@example.com:password'  https://api.feedbin.com/v2/subscriptions/3.json
< ETag: "c7d001e87bda1f0d3745b6bd2811b055"
< Last-Modified: Sat, 02 Feb 2013 15:20:46 GMT
```

You can use these headers in subsequent requests like:

```shell
curl -v -u 'example@example.com:password' --header 'If-Modified-Since:Sat, 02 Feb 2013 15:20:46 GMT' --header 'If-None-Match:"c7d001e87bda1f0d3745b6bd2811b055"' https://api.feedbin.com/v2/subscriptions/3.json
< HTTP/1.1 304 Not Modified
```

Pagination
----------
Entries use pagination. Each page has a limit of 100 items. Paginated request will include a link header like:

```
Links: <https://api.feedbin.com/v2/feeds/1/entries.json?page=2>; rel="next", <https://api.feedbin.com/v2/feeds/1/entries.json?page=5>; rel="last"
```

The possible rel values are:

- `first` The URL of the first page of results.
- `prev` The URL of the previous page of results.
- `next` The URL of the next page of results.
- `last` The URL of the last page of results.

On paginated resources there is a header in the response called: `X-Feedbin-Record-Count`. This header reports the total number of records for a resource.

Dates
-----
The Feedbin API uses the [ISO 8601](http://www.w3.org/TR/NOTE-datetime) date format. All responses will include dates formatted to this spec and all requests should stick to it as well. The dates are as high resolution as possible to allow for rapid state changes. When using the `since` parameter it is best to include the date exactly as it was returned by the server when the last request was made. Rounding down to the nearest second will most likely cause duplicates.

The date should include complete date plus hours, minutes, seconds and timezone `YYYY-MM-DDThh:mm:ss.ssssssTZD` (eg `2013-02-19T07:33:38.449047-08:00` or in UTC `2013-02-19T15:33:38.449047Z`). All dates will be converted to UTC, so the timezone is very important.

**Note**

In Objective-C it's important to force a locale for the date because different regions can cause unexpected output. For example you can properly format a date for the Feedbin API like:

```objectivec
NSDateFormatter *feedbinDateFormatter = [[NSDateFormatter alloc] init];
feedbinDateFormatter.timeZone = [NSTimeZone timeZoneWithAbbreviation:@"GMT"];
[feedbinDateFormatter setDateFormat:@"yyyy-MM-dd'T'HH:mm:ss.SSSSSS'Z'"];
[feedbinDateFormatter setLocale:[[NSLocale alloc] initWithLocaleIdentifier:@"en_US"]];
```

Thanks to [Stefan Pauwels](http://zoziapps.ch/) for sharing this tip.

Domain
------

Until 2014-03-14 the API hostname was `api.feedbin.me`. `api.feedbin.me` will remain available but `api.feedbin.com` is recommended because it is the new primary domain.
