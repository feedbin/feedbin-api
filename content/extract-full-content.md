Extracting Full Content
=======================

If you have a native app that supports Feedbin, you can use Feedbin's full content service.

The service uses [Mercury Parser](https://github.com/postlight/mercury-parser) to attempt to extract the full content of a webpage.

In order to use the service, you need a username and signing key. The signing key is used to generate an HMAC-SHA1 signature to authenticate your request.

An example request looks like:

```
https://extract.feedbin.com/parser/:username/:signature?base64_url=:base64_url
```

The parts that you need are:

- `username` your username
- `signature` the HMAC-SHA1 signature of the URL you want to parse
- `base64_url` base64 encoded version of the URL you want to parse

The URL is base64 encoded to avoid any issues in the way different systems encode URLs. It must use the [RFC 4648](https://tools.ietf.org/html/rfc4648#section-5) url-safe variant with no newlines.

If your platform does not offer a URL safe base64 option, you can replicate it. First create the base64 encoded string. Then replace the following characters:

- `+` => `-`
- `/` => `_`
- `\n` => ""


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

With the output:

```json
{
    "title": "Private by Default",
    "author": null,
    "date_published": "2018-09-11T00:00:00.000Z",
    "dek": null,
    "lead_image_url": "https://assets.feedbin.com/assets-site/blog/2018-09-11/embed-3f43088538ae5ed7e585c00013adc13a915fd35de31990b3081a085b963ed7dd.png",
    "content": "<div>content</div>",
    "next_page_url": null,
    "url": "https://feedbin.com/blog/2018/09/11/private-by-default/",
    "domain": "feedbin.com",
    "excerpt": "September 11, 2018 by Ben Ubois I want Feedbin to be the opposite of Big Social. I think people should have the right not to be tracked on the Internet and Feedbin can help facilitate that. Since&hellip;",
    "word_count": 787,
    "direction": "ltr",
    "total_pages": 1,
    "rendered_pages": 1
}
```

You can use this as a reference for matching your implementation.
