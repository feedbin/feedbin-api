Authentication
==============

### `GET /v2/authentication.json`

Returns status code. You can check a users credentials with this endpoint.

```bash
curl --request GET --user "example@example.com:password" https://api.feedbin.com/v2/authentication.json
```

You'll need to include the credentials using HTTP basic auth. You can set this through the `Authorization` header or using your favorite HTTP library's built in support for it.

**Status Codes**

- `200 OK` will be returned if credentials are valid
- `401 Unauthorized` will be returned  if credentials are invalid
