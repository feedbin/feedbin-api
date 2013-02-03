Feedbin API
===========

Making Requests
---------------

The base URL for all requests is `https://feedbin.me/api/v1/` Only https is supported.

The Feedbin API uses HTTP Basic authentication

Using cURL you would make a request like: 

```shell
curl -u 'example@example.com:password' https://feedbin.me/api/v1/subscriptions.json
```

When creating or updating a record you must set `application/json; charset=utf-8` as the `Content-Type` header.

```shell
curl -u 'ben+1@benubois.com:passw0rd' \
-H "Content-Type: application/json; charset=utf-8" \
-X POST -d '{"feed_url":"http://daringfireball.net"}' \
http://feedbin.dev/api/v1/subscriptions.json
```

Without this header you'll wind up with a `415 Unsupported Media Type` response.

API Objects
-----------

- [Subscriptions](content/subscriptions.md)