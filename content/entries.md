Entries
=======

You can get all entries for a user sorted by `created_at` descending. The entry attributes vary from the original feed in several ways. Links and image sources are rewritten to always point to the fully qualified URL. This means sanitizing/escaping content is up to you. The `published` date is converted to UTC.

### `GET /v2/entries.json`

Returns a paginated array of all entries for the user.

```bash
curl --request GET --user "example@example.com:password" https://api.feedbin.com/v2/entries.json
```

```json
[
  {
    "id": 2077,
    "feed_id": 135,
    "title": "Objective-C Runtime Releases",
    "url": "http:\/\/mjtsai.com\/blog\/2013\/02\/02\/objective-c-runtime-releases\/",
    "extracted_content_url": "https://extract.feedbin.com/parser/feedbin/9197b49979d10d5012130f8b456bd5bd040d3206?base64_url=aHR0cDovL3d3dy5jcmFpZ2tlcnN0aWVucy5jb20vMjAxNy8wMy8xMi9nZXR0aW5nLXN0YXJ0ZWQtd2l0aC1qc29uYi1pbi1wb3N0Z3Jlcy8=",
    "author": "Michael Tsai",
    "content": "<p><a href=\"https:\/\/twitter.com\/bavarious\/status\/297851496945577984\">Bavarious<\/a> created a <a href=\"https:\/\/github.com\/bavarious\/objc4\/commits\/master\">GitHub repository<\/a> that shows the differences between versions of <a href=\"http:\/\/www.opensource.apple.com\/source\/objc4\/\">Apple\u2019s Objective-C runtime<\/a> that shipped with different versions of Mac OS X.<\/p>",
    "summary": "Bavarious created a GitHub repository that shows the differences between versions of Apple\u2019s Objective-C runtime that shipped with different versions of Mac OS X.",
    "published": "2013-02-03T01:00:19.000000Z",
    "created_at": "2013-02-04T01:00:19.127893Z"
  }
]
```

Note that `title`, `author`, and `content` can be null. For example, using this feed:

```xml
<?xml version="1.0" encoding="utf-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
  <id>urn:uuid:60a76c80-d399-11d9-b93C-0003939e0af6</id>
  <entry>
    <id>urn:uuid:1225c695-cfb8-4ebb-aaaa-80da344efa6a</id>
  </entry>
</feed>
```

```json
[{
    "id": 1570169709,
    "feed_id": 1356310,
    "title": null,
    "author": null,
    "summary": "",
    "content": null,
    "url": "http://s3.amazonaws.com",
    "extracted_content_url": "https://extract.feedbin.com/parser/feedbin/9197b49979d10d5012130f8b456bd5bd040d3206?base64_url=aHR0cDovL3d3dy5jcmFpZ2tlcnN0aWVucy5jb20vMjAxNy8wMy8xMi9nZXR0aW5nLXN0YXJ0ZWQtd2l0aC1qc29uYi1pbi1wb3N0Z3Jlcy8=",
    "published": "2017-10-28T14:54:19.885152Z",
    "created_at":"2017-10-28T14:54:19.885105Z"
}]
```

| Parameter                       | Required | Example                                                                                                                                           |
| ------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `page: number`                  | false    | `GET /v2/entries.json?page=2`  will get page two of the available entries                                                                         |
| `since: date`                   | false    | `GET /v2/entries.json?since=2013-02-02T14:07:33.000000Z` will get all entries created after the iso 8601 timestamp.                               |
| `ids: number(s)`                | false    | `GET /v2/entries.json?ids=1,2,3`  will get the entries with the ids 1, 2 and 3. A maximum of 100 entries can be requested.                        |
| `read: boolean`                 | false    | `GET /v2/entries.json?read=false`  will get all unread entries.                                                                                   |
| `starred: boolean`              | false    | `GET /v2/entries.json?starred=true`  will get all starred entries.                                                                                |
| `per_page: number`              | false    | `GET /v2/entries.json?per_page=50`  will limit results to 50 per page.                                                                            |
| `mode: enum`                    | false    | `GET /v2/entries.json?mode=extended`  the only mode available is `extended`. This includes more metadata for the entry                            |
| `include_original: boolean`     | false    | `GET /v2/entries.json?include_original=true`  include original entry data if the entry has been updated.                                          |
| `include_enclosure: boolean`    | false    | `GET /v2/entries.json?include_enclosure=true`  include podcast/RSS enclosure data.                                                                |
| `include_content_diff: boolean` | false    | `GET /v2/entries.json?include_content_diff=true`  include a diff of changed content. Result is HTML marked up to show differences. [Sample styles](https://github.com/feedbin/feedbin/blob/2610ba5aed103789d2a61708ffcd10d0432b5161/app/assets/stylesheets/_site.scss#L3246-L3309). |

#### About `extracted_content_url`

The `extracted_content_url` is the link to another [Feedbin service](https://feedbin.com/blog/2019/03/11/the-future-of-full-content/) that attempts to extract the full content of the entry `url`. It is powered by [Mercury Parser](https://github.com/postlight/mercury-parser) and returns the same JSON object that Mercury uses.

```json
{
  "title": "Thunder (mascot)",
  "content": "... <p><b>Thunder</b> is the <a href=\"https://en.wikipedia.org/wiki/Stage_name\">stage name</a> for the...",
  "author": "Wikipedia Contributors",
  "date_published": "2016-09-16T20:56:00.000Z",
  "lead_image_url": null,
  "dek": null,
  "next_page_url": null,
  "url": "https://en.wikipedia.org/wiki/Thunder_(mascot)",
  "domain": "en.wikipedia.org",
  "excerpt": "Thunder Thunder is the stage name for the horse who is the official live animal mascot for the Denver Broncos",
  "word_count": 4677,
  "direction": "ltr",
  "total_pages": 1,
  "rendered_pages": 1
}
```

#### About `extended` Mode

The `extended` mode includes a lot of additional meta-data for entries including the usual `id`, `feed_id`, `title`, `author`, `summary`, `content`, `url`, `published`, `created_at`. As well as these additions:

- `original`: The JSON for the full original entry, if this entry has been updated
- `images`: The image that Feedbin has extracted to be associated with the entry.
- `enclosure`: Podcast related metadata
- `twitter_id`: If the entry is a tweet, this is the id of the tweet on twitter. You can use this with the Twitter API to load tweets in your app.
- `twitter_thread_ids`: If the entry has a related Twitter thread, this array of ids can be used with the Twitter API to load to load the full thread. The ids are sorted in ascending chronological order.
- `extracted_articles`: If the entry is a tweet that links to articles, Feedbin attempts to extract the article content and provides it via the API.
- `json_feed`: If the entry is from a JSON Feed, this contains the additional metadata that [JSON Feed offers](https://jsonfeed.org/version/1).


Extended mode was created to make sure the original data would stay the same. The `extended` mode has a different policy where new data may be added over time. The only thing to keep in mind here is that there may be additional keys in the future and that your JSON parser should be flexible enough to deal with that. Keys will not be removed and their purpose will not change.

An example with all of the keys populated would look like:

```json
{
    "id": 1682191545,
    "feed_id": 1379740,
    "title": "Peter Kafka @pkafka",
    "author": "Peter Kafka",
    "summary": "In 2009, the big magazine publishers built their own digital service so they wouldn't be cut out by Apple or Google. Now they're selling to Apple.",
    "content": "<div>Content</div>",
    "url": "https://twitter.com/fromedome/status/973315765393920000",
    "extracted_content_url": "https://extract.feedbin.com/parser/feedbin/9197b49979d10d5012130f8b456bd5bd040d3206?base64_url=aHR0cDovL3d3dy5jcmFpZ2tlcnN0aWVucy5jb20vMjAxNy8wMy8xMi9nZXR0aW5nLXN0YXJ0ZWQtd2l0aC1qc29uYi1pbi1wb3N0Z3Jlcy8=",
    "published": "2018-03-12T21:52:16.000000Z",
    "created_at": "2018-03-12T22:55:53.437304Z",
    "original": {
        "author": "Brent Simmons",
        "content": "<div>Content</div>",
        "title": "Catching Up on The Omni Show",
        "url": "https://www.omnigroup.com/blog/entry/catching-up-on-the-omni-show",
        "entry_id": "https://www.omnigroup.com/blog/entry/catching-up-on-the-omni-show",
        "published": "2018-03-12T21:24:00.000Z",
        "data": {}
    },
    "twitter_id": 973315765393920000,
    "twitter_thread_ids": [973315765393920000, 973315765393920001],
    "images": {
        "original_url": "http://www.macdrifter.com/uploads/2018/03/ScreenShot20180312_044129.jpg",
        "size_1": {
            "cdn_url": "https://images.feedbinusercontent.com/85996e1/85996e10ef95a3b96a914e67dfc08d5d3362c6e0.jpg",
            "width": 542,
            "height": 304
        }
    },
    "enclosure": {
        "enclosure_url": "http://traffic.libsyn.com/atpfm/atp264.mp3",
        "enclosure_type": "audio/mpeg",
        "enclosure_length": "54103635",
        "itunes_duration": "01:51:35",
        "itunes_image": "http://static1.squarespace.com/static/513abd71e4b0fe58c655c105/t/52c45a37e4b0a77a5034aa84/1388599866232/1500w/Artwork.jpg"
    },
    "extracted_articles": [
        {
            "url": "https://www.recode.net/2018/3/12/17109592/apple-buys-texture-magazine-next-issue-media-eddy-cue-sxsw?utm_campaign=recode.net&utm_content=chorus&utm_medium=social&utm_source=twitter",
            "title": "Apple is buying Texture, the digital magazine distributor",
            "host": "www.recode.net",
            "author": "Peter Kafka",
            "content": "<div>Content</div>"
        }
    ]
}
```

### `GET /v2/feeds/203/entries.json`

Returns a paginated array of all entries in feed_id 203

```bash
curl --request GET --user "example@example.com:password" https://api.feedbin.com/v2/feeds/203/entries.json
```

```json
[
  {
    "id": 3648,
    "feed_id": 203,
    "title": "Cleveland Drinkup February 6",
    "url": "https:\/\/github.com\/blog\/1398-cleveland-drinkup-february-6",
    "extracted_content_url": "https://extract.feedbin.com/parser/feedbin/9197b49979d10d5012130f8b456bd5bd040d3206?base64_url=aHR0cDovL3d3dy5jcmFpZ2tlcnN0aWVucy5jb20vMjAxNy8wMy8xMi9nZXR0aW5nLXN0YXJ0ZWQtd2l0aC1qc29uYi1pbi1wb3N0Z3Jlcy8=",
    "author": "juliamae",
    "content": "<p>Cleveland <img class=\"emoji\" title=\":metal:\" alt=\":metal:\" src=\"https:\/\/a248.e.akamai.net\/assets.github.com\/images\/icons\/emoji\/metal.png\" height=\"20\" width=\"20\" align=\"absmiddle\">! Let's <img class=\"emoji\" title=\":beers:\" alt=\":beers:\" src=\"https:\/\/a248.e.akamai.net\/assets.github.com\/images\/icons\/emoji\/beers.png\" height=\"20\" width=\"20\" align=\"absmiddle\"><img class=\"emoji\" title=\":cocktail:\" alt=\":cocktail:\" src=\"https:\/\/a248.e.akamai.net\/assets.github.com\/images\/icons\/emoji\/cocktail.png\" height=\"20\" width=\"20\" align=\"absmiddle\"><img class=\"emoji\" title=\":neckbeard:\" alt=\":neckbeard:\" src=\"https:\/\/a248.e.akamai.net\/assets.github.com\/images\/icons\/emoji\/neckbeard.png\" height=\"20\" width=\"20\" align=\"absmiddle\"><img class=\"emoji\" title=\":guitar:\" alt=\":guitar:\" src=\"https:\/\/a248.e.akamai.net\/assets.github.com\/images\/icons\/emoji\/guitar.png\" height=\"20\" width=\"20\" align=\"absmiddle\"><img class=\"emoji\" title=\":octocat:\" alt=\":octocat:\" src=\"https:\/\/a248.e.akamai.net\/assets.github.com\/images\/icons\/emoji\/octocat.png\" height=\"20\" width=\"20\" align=\"absmiddle\"> in one of Ohio's greatest cities, Cleveland!<\/p>\n\n<p>Join <a href=\"https:\/\/github.com\/asenchi\" class=\"user-mention\">@asenchi<\/a> and me Wednesday at the <a href=\"http:\/\/www.yelp.com\/biz\/great-lakes-brewing-company-cleveland-4\">Great Lakes Brewing Company Taproom<\/a>, drinks on GitHub.<\/p>\n\n<p><img src=\"https:\/\/f.cloud.github.com\/assets\/849\/119266\/79ef6bbe-6c9e-11e2-9150-47d7da0b85c9.jpg\" alt=\"Great Lakes Taproom\"><\/p>\n\n<p><strong>The Facts:<\/strong><\/p>\n\n<ul>\n<li>\n<a href=\"http:\/\/www.greatlakesbrewing.com\/brewpub\/around-the-brewpub\">Great Lakes Brewing Company<\/a> - <a href=\"https:\/\/maps.google.com\/?q=2516+Market+Ave,+Cleveland,+OH,+USA\">2516 Market Ave<\/a>\n<\/li>\n<li>Wednesday, February 6 at 8:00pm<\/li>\n<\/ul><p><a href=\"https:\/\/maps.google.com\/?q=2516+Market+Ave,+Cleveland,+OH,+USA\"><img src=\"https:\/\/f.cloud.github.com\/assets\/849\/119328\/c8cbb682-6ca0-11e2-81c8-246e4027f892.png\" alt=\"Screen Shot 2013-02-01 at 1 53 02 PM\"><\/a>          <\/p>",
    "summary": null,
    "published": "2013-02-03T01:00:19.000000Z",
    "created_at": "2013-02-04T01:00:19.127893Z"
  }
]
```

**Parameters**

Supports the same parameters as `/v2/entries.json`, except the `ids` parameter.

**Status Codes**

- `200 OK` will be returned if found
- `404 Not Found` will be returned if no feed is found, or if the page number does not exist
- `403 Forbidden` will be returned if the user does not subscribe to this feed

### `GET /v2/entries/3648.json`

```bash
curl --request GET --user "example@example.com:password" https://api.feedbin.com/v2/entries/3648.json
```

Returns a single entry object for id 3648

```json
{
  "id": 3648,
  "feed_id": 203,
  "title": "Cleveland Drinkup February 6",
  "url": "https:\/\/github.com\/blog\/1398-cleveland-drinkup-february-6",
  "extracted_content_url": "https://extract.feedbin.com/parser/feedbin/9197b49979d10d5012130f8b456bd5bd040d3206?base64_url=aHR0cDovL3d3dy5jcmFpZ2tlcnN0aWVucy5jb20vMjAxNy8wMy8xMi9nZXR0aW5nLXN0YXJ0ZWQtd2l0aC1qc29uYi1pbi1wb3N0Z3Jlcy8=",
  "author": "juliamae",
  "content": "<p>Cleveland <img class=\"emoji\" title=\":metal:\" alt=\":metal:\" src=\"https:\/\/a248.e.akamai.net\/assets.github.com\/images\/icons\/emoji\/metal.png\" height=\"20\" width=\"20\" align=\"absmiddle\">! Let's <img class=\"emoji\" title=\":beers:\" alt=\":beers:\" src=\"https:\/\/a248.e.akamai.net\/assets.github.com\/images\/icons\/emoji\/beers.png\" height=\"20\" width=\"20\" align=\"absmiddle\"><img class=\"emoji\" title=\":cocktail:\" alt=\":cocktail:\" src=\"https:\/\/a248.e.akamai.net\/assets.github.com\/images\/icons\/emoji\/cocktail.png\" height=\"20\" width=\"20\" align=\"absmiddle\"><img class=\"emoji\" title=\":neckbeard:\" alt=\":neckbeard:\" src=\"https:\/\/a248.e.akamai.net\/assets.github.com\/images\/icons\/emoji\/neckbeard.png\" height=\"20\" width=\"20\" align=\"absmiddle\"><img class=\"emoji\" title=\":guitar:\" alt=\":guitar:\" src=\"https:\/\/a248.e.akamai.net\/assets.github.com\/images\/icons\/emoji\/guitar.png\" height=\"20\" width=\"20\" align=\"absmiddle\"><img class=\"emoji\" title=\":octocat:\" alt=\":octocat:\" src=\"https:\/\/a248.e.akamai.net\/assets.github.com\/images\/icons\/emoji\/octocat.png\" height=\"20\" width=\"20\" align=\"absmiddle\"> in one of Ohio's greatest cities, Cleveland!<\/p>\n\n<p>Join <a href=\"https:\/\/github.com\/asenchi\" class=\"user-mention\">@asenchi<\/a> and me Wednesday at the <a href=\"http:\/\/www.yelp.com\/biz\/great-lakes-brewing-company-cleveland-4\">Great Lakes Brewing Company Taproom<\/a>, drinks on GitHub.<\/p>\n\n<p><img src=\"https:\/\/f.cloud.github.com\/assets\/849\/119266\/79ef6bbe-6c9e-11e2-9150-47d7da0b85c9.jpg\" alt=\"Great Lakes Taproom\"><\/p>\n\n<p><strong>The Facts:<\/strong><\/p>\n\n<ul>\n<li>\n<a href=\"http:\/\/www.greatlakesbrewing.com\/brewpub\/around-the-brewpub\">Great Lakes Brewing Company<\/a> - <a href=\"https:\/\/maps.google.com\/?q=2516+Market+Ave,+Cleveland,+OH,+USA\">2516 Market Ave<\/a>\n<\/li>\n<li>Wednesday, February 6 at 8:00pm<\/li>\n<\/ul><p><a href=\"https:\/\/maps.google.com\/?q=2516+Market+Ave,+Cleveland,+OH,+USA\"><img src=\"https:\/\/f.cloud.github.com\/assets\/849\/119328\/c8cbb682-6ca0-11e2-81c8-246e4027f892.png\" alt=\"Screen Shot 2013-02-01 at 1 53 02 PM\"><\/a>          <\/p>",
  "summary": null,
  "published": "2013-02-03T01:00:19.000000Z",
  "created_at": "2013-02-04T01:00:19.127893Z"
}
```

**Status Codes**

- `200 OK` will be returned if found
- `404 Not Found` will be returned if no entry is found
- `403 Forbidden` will be returned if the user does not subscribe to the feed this entry belongs to

Sample Responses
----------------

**include_original**

`GET /v2/entries/696388086.json?include_original=true`

```json
{
  "id": 696388086,
  "feed_id": 47,
  "title": "Audio Hijack 3",
  "author": "John Gruber",
  "content": "<p>Gorgeous new interface in this major update to Rogue Amoeba&#8217;s venerable audio recording app. This is one of the best takes on Yosemite-style design I&#8217;ve seen.<\/p> <p><strong>See also:<\/strong> <a href=\"http:\/\/sixcolors.com\/post\/2015\/01\/audio-hijack-3-a-huge-amazing-update\/\">Jason Snell&#8217;s take on the app and interview with Paul Kafasis<\/a>.<\/p> <div> <a title=\"Permanent link to ‘Audio Hijack 3’\" href=\"http:\/\/daringfireball.net\/linked\/2015\/01\/20\/audio-hijack-3\">&nbsp;★&nbsp;<\/a> <\/div>",
  "summary": null,
  "url": "http:\/\/weblog.rogueamoeba.com\/2015\/01\/20\/audio-hijack-3-has-arrived\/",
  "extracted_content_url": "https://extract.feedbin.com/parser/feedbin/9197b49979d10d5012130f8b456bd5bd040d3206?base64_url=aHR0cDovL3d3dy5jcmFpZ2tlcnN0aWVucy5jb20vMjAxNy8wMy8xMi9nZXR0aW5nLXN0YXJ0ZWQtd2l0aC1qc29uYi1pbi1wb3N0Z3Jlcy8=",
  "published": "2015-01-21T01:34:41.000000Z",
  "created_at": "2015-01-21T01:37:57.679046Z",
  "original": {
    "author": "John Gruber",
    "content": "<p>Gorgeous new interface in this major update to Rogue Amoeba&#8217;s venerable audio recording app. This is one of the best takes on Yosemite-style design I&#8217;ve seen.<\/p> <div> <a title=\"Permanent link to ‘Audio Hijack 3’\" href=\"http:\/\/daringfireball.net\/linked\/2015\/01\/20\/audio-hijack-3\">&nbsp;★&nbsp;<\/a> <\/div>",
    "title": "Audio Hijack 3",
    "url": "http:\/\/weblog.rogueamoeba.com\/2015\/01\/20\/audio-hijack-3-has-arrived\/",
    "entry_id": "tag:daringfireball.net,2015:/linked//6.30480",
    "published": "2015-01-21T01:34:41.000Z",
    "data": null
  }
}
```

**include_enclosure**

`GET /v2/entries.json?include_enclosure=true`

```json
{
  "id": 683590343,
  "feed_id": 908904,
  "title": "99: Pop-Up Headlights",
  "author": null,
  "content": "<ul> <li>Follow-Up: <ul><li>SSL <ul><li>In schools &amp; corporations<\/li> <li><a href=\"http:\/\/www.gogoair.com\/\">Gogo<\/a> actually <a href=\"http:\/\/www.neowin.net\/news\/gogo-inflight-internet-is-intentionally-issuing-fake-ssl-certificates\">issues their own certificates to intercept SSL<\/a><\/li> <li><a href=\"https:\/\/en.wikipedia.org\/wiki\/SOCKS\">SOCKS<\/a><\/li><\/ul><\/li> <li>Using C# outside Windows (via <a href=\"https:\/\/twitter.com\/praeclarum\/status\/551517070186541056\">Frank A. Krueger<\/a>)<\/li> <li>Marco's <a href=\"https:\/\/golang.org\">Go<\/a> feed poller <a href=\"https:\/\/twitter.com\/marcoarment\/status\/552202315181326336\">update<\/a> <ul><li><a href=\"https:\/\/en.wikipedia.org\/wiki\/Integrated_development_environment\">IDE<\/a><\/li> <li><a href=\"http:\/\/www.eclipse.org\">Eclipse<\/a><\/li> <li><a href=\"http:\/\/www.rust-lang.org\">Rust<\/a><\/li> <li><a href=\"http:\/\/en.wikipedia.org\/wiki\/Communicating_sequential_processes\">Communicating sequential processes<\/a><\/li><\/ul><\/li><\/ul><\/li> <li>Apple's Software Quality <ul><li><a href=\"http:\/\/www.marco.org\/2015\/01\/04\/apple-lost-functional-high-ground\">Marco's post<\/a><\/li> <li><a href=\"http:\/\/www.marco.org\/2015\/01\/05\/popular-for-a-day\">Marco's retrospective<\/a><\/li> <li><a href=\"http:\/\/video.cnbc.com\/gallery\/?video=3000343764\">Mention on CNBC<\/a><\/li> <li><a href=\"http:\/\/5by5.tv\/hypercritical\/55\">Hypercritical #55<\/a><\/li> <li><a href=\"http:\/\/www.caseyliss.com\/2015\/1\/5\/bravery\">Casey's response to Marco<\/a><\/li> <li><a href=\"http:\/\/glog.glennf.com\/blog\/2015\/1\/6\/the-software-and-services-apple-needs-to-fix\">Glenn Fleishman's list<\/a><\/li><\/ul><\/li> <li>How to write for understanding <ul><li><a href=\"http:\/\/www.marco.org\/2013\/12\/29\/apple-doesnt-have-time\">Marco laments about software quality in the past<\/a><\/li><\/ul><\/li> <li><a href=\"http:\/\/9to5mac.com\/2015\/01\/06\/macbook-air-12-inch-redesign\/\">Rumored 12\" MacBook Air<\/a> <ul><li><a href=\"https:\/\/www.twelvesouth.com\/product\/plugbug\">PlugBug<\/a><\/li> <li><a href=\"https:\/\/twitter.com\/chockenberry\/status\/552928449250078721\">Chockenberry on a potential ARM transition<\/a><\/li> <li><a href=\"https:\/\/en.wikipedia.org\/wiki\/Fat_binary\">Fat binary<\/a><\/li> <li>Special thanks to <a href=\"http:\/\/david-smith.org\/\">_DavidSmith<\/a> for finding \"bezels\" in <a href=\"http:\/\/5by5.tv\/hypercritical\/22\">Hypercritical #22<\/a><\/li><\/ul><\/li> <\/ul> <p>Sponsored by:<\/p> <ul> <li><a href=\"http:\/\/automatic.com\/atp\">Automatic<\/a>: Your smart driving assistant. Get $20 off with this link.<\/li> <li><a href=\"http:\/\/hover.com\/atp\">Hover<\/a>: The best way to buy and manage domain names. Use coupon code <strong>HIGHGROUND<\/strong> for 10% off.<\/li> <li><a href=\"https:\/\/caspersleep.com\/atp\">Casper<\/a>: A mattress with just the right sink, just the right bounce, for better nights and brighter days. Use code <strong>ATP<\/strong> for $50 off.<\/li> <\/ul>",
  "summary": null,
  "url": "http:\/\/atp.fm\/episodes\/99",
  "extracted_content_url": "https://extract.feedbin.com/parser/feedbin/9197b49979d10d5012130f8b456bd5bd040d3206?base64_url=aHR0cDovL3d3dy5jcmFpZ2tlcnN0aWVucy5jb20vMjAxNy8wMy8xMi9nZXR0aW5nLXN0YXJ0ZWQtd2l0aC1qc29uYi1pbi1wb3N0Z3Jlcy8=",
  "published": "2015-01-09T20:11:41.000000Z",
  "created_at": "2015-01-09T23:54:57.672303Z",
  "enclosure": {
    "enclosure_type": "audio/mpeg",
    "enclosure_url": "http:\/\/traffic.libsyn.com\/atpfm\/atp99.mp3",
    "enclosure_length": "86528647",
    "itunes_duration": "02:00:00"
  }
}
```
