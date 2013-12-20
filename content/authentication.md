Authentication
==============

Get authentication
------------------

You can check a users credentials with this endpoint.

- `GET /v2/authentication.json`

You'll need to include the credentials using HTTP basic auth. You can set this through the `Authorization` header or using your favorite HTTP library's built in support for it i.e.

```bash
curl -u 'example@example.com:password' https://api.feedbin.me/v2/authentication.json
```

**Status Codes**

- `200 OK` will be returned if credentials are valid
- `401 Unauthorized` will be returned  if credentials are invalid
