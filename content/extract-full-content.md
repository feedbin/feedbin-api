Extracting Full Content
=======================

If you have a native app that supports Feedbin, you can use Feedbin's full content service.

The service uses [Mercury Parser](https://github.com/postlight/mercury-parser) to attempt to extract the full content of a webpage.

In order to use the service, you need a username and signing key. The signing key is used to generate an HMAC signature to authenticate your request.

An example request looks like:

```
https://extract.feedbin.com/parser/:username/:signature?base64_url=:base64_encoded_url
```

The parts that you need are:

`username`: your username
`signature`: the HMAC signature of the URL you want to parse
`base64_encoded_url`: base64 encoded version of the URL you want to parse

The URL is base64 encoded to avoid any issues in the way different systems encode URLs. It must use the [RFC 4648](https://tools.ietf.org/html/rfc4648#section-5) url-safe variant with no newlines.

If your platform does not offer a URL safe base64 option, you can replicate it. First create the base64 encoded string. Then replace the following characters:

`+` => `-`
`/` => `_`
`\n` => ``


```ruby
require "uri"
require "openssl"
require "base64"

username = "username"
secret = "secret"
url = "https://feedbin.com/blog/2018/09/11/private-by-default/"

digest = OpenSSL::Digest.new("sha1")
signature = OpenSSL::HMAC.hexdigest(digest, secret, url)

base64_url = Base64.urlsafe_encode64(url).gsub("\n", "")

URI::HTTPS.build({
  host: "extract.feedbin.com",
  path: "/parser/#{username}/#{signature}",
  query: "base64_url=#{base64_url}"
}).to_s
```

The above example would produce:

```
https://extract.feedbin.com/parser/username/e4696f8630bb68c21d77a9629ce8d063d8e5f81c?base64_url=aHR0cHM6Ly9mZWVkYmluLmNvbS9ibG9nLzIwMTgvMDkvMTEvcHJpdmF0ZS1ieS1kZWZhdWx0Lw==
```

You can use this as a reference for matching your implementation.