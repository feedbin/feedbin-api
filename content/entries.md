Entries
=======

Get Entries
-----------

You can get all entries for a user sorted by `created_at` descending. The entry attributes vary from the original feed in several ways. Links and image sources are rewritten to always point to the fully qualified URL. This means sanitizing/escaping content is up to you. The `published` date is converted to UTC.

- `GET /v2/entries.json` will return all entries for the user.

```json
[
  {
    "id": 2077,
    "feed_id": 135,
    "title": "Objective-C Runtime Releases",
    "url": "http:\/\/mjtsai.com\/blog\/2013\/02\/02\/objective-c-runtime-releases\/",
    "author": "Michael Tsai",
    "content": "<p><a href=\"https:\/\/twitter.com\/bavarious\/status\/297851496945577984\">Bavarious<\/a> created a <a href=\"https:\/\/github.com\/bavarious\/objc4\/commits\/master\">GitHub repository<\/a> that shows the differences between versions of <a href=\"http:\/\/www.opensource.apple.com\/source\/objc4\/\">Apple\u2019s Objective-C runtime<\/a> that shipped with different versions of Mac OS X.<\/p>",
    "summary": "Bavarious created a GitHub repository that shows the differences between versions of Apple\u2019s Objective-C runtime that shipped with different versions of Mac OS X.",
    "published": "2013-02-03T01:00:19.000000Z",
    "created_at": "2013-02-04T01:00:19.127893Z"
  }
]
```

| Parameter                    | Required | Example                                                                                                             |
| ---------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------- |
| `page: number`               | false    | `GET /v2/entries.json?page=2`  will get page two of the available entries                                           |
| `since: date`                | false    | `GET /v2/entries.json?since=2013-02-02T14:07:33.000000Z` will get all entries created after the iso 8601 timestamp. |
| `starred: boolean`           | false    | `GET /v2/entries.json?starred=true`  will get all starred entries.                                                  |
| `ids: number(s)`             | false    | `GET /v2/entries.json?ids=1,2,3`  will get the entries with the ids 1, 2 and 3.                                     |
| `per_page: number`           | false    | `GET /v2/entries.json?per_page=50`  will limit results to 50 per page.                                              |
| `include_original: boolean`  | false    | `GET /v2/entries.json?include_original=true`  include original entry data if the entry has been updated.            |
| `include_enclosure: boolean` | false    | `GET /v2/entries.json?include_enclosure=true`  include podcast/RSS enclosure data.                                  |


Entries belong to feeds. To get all the entries for a feed use the `feed_id`.

- `GET /v2/feeds/203/entries.json` will return all entries for feed `203`

```json
[
  {
    "id": 3648,
    "feed_id": 203,
    "title": "Cleveland Drinkup February 6",
    "url": "https:\/\/github.com\/blog\/1398-cleveland-drinkup-february-6",
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

Get Entry
---------

- `GET /v2/entries/3648.json` will return just entry `3648`

```json
{
  "id": 3648,
  "feed_id": 203,
  "title": "Cleveland Drinkup February 6",
  "url": "https:\/\/github.com\/blog\/1398-cleveland-drinkup-february-6",
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
  "content": "<p>Gorgeous new interface in this major update to Rogue Amoeba&#8217;s venerable audio recording app. This is one of the best takes on Yosemite-style design I&#8217;ve seen.</p> <p><strong>See also:</strong> <a href="http://sixcolors.com/post/2015/01/audio-hijack-3-a-huge-amazing-update/">Jason Snell&#8217;s take on the app and interview with Paul Kafasis</a>.</p> <div> <a title="Permanent link to ‘Audio Hijack 3’" href="http://daringfireball.net/linked/2015/01/20/audio-hijack-3">&nbsp;★&nbsp;</a> </div>",
  "summary": null,
  "url": "http://weblog.rogueamoeba.com/2015/01/20/audio-hijack-3-has-arrived/",
  "published": "2015-01-21T01:34:41.000000Z",
  "created_at": "2015-01-21T01:37:57.679046Z",
  "original": {
    "author": "John Gruber",
    "content": "<p>Gorgeous new interface in this major update to Rogue Amoeba&#8217;s venerable audio recording app. This is one of the best takes on Yosemite-style design I&#8217;ve seen.</p> <div> <a title="Permanent link to ‘Audio Hijack 3’" href="http://daringfireball.net/linked/2015/01/20/audio-hijack-3">&nbsp;★&nbsp;</a> </div>",
    "title": "Audio Hijack 3",
    "url": "http://weblog.rogueamoeba.com/2015/01/20/audio-hijack-3-has-arrived/",
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
  "content": "<ul> <li>Follow-Up: <ul><li>SSL <ul><li>In schools &amp; corporations</li> <li><a href="http://www.gogoair.com/">Gogo</a> actually <a href="http://www.neowin.net/news/gogo-inflight-internet-is-intentionally-issuing-fake-ssl-certificates">issues their own certificates to intercept SSL</a></li> <li><a href="https://en.wikipedia.org/wiki/SOCKS">SOCKS</a></li></ul></li> <li>Using C# outside Windows (via <a href="https://twitter.com/praeclarum/status/551517070186541056">Frank A. Krueger</a>)</li> <li>Marco's <a href="https://golang.org">Go</a> feed poller <a href="https://twitter.com/marcoarment/status/552202315181326336">update</a> <ul><li><a href="https://en.wikipedia.org/wiki/Integrated_development_environment">IDE</a></li> <li><a href="http://www.eclipse.org">Eclipse</a></li> <li><a href="http://www.rust-lang.org">Rust</a></li> <li><a href="http://en.wikipedia.org/wiki/Communicating_sequential_processes">Communicating sequential processes</a></li></ul></li></ul></li> <li>Apple's Software Quality <ul><li><a href="http://www.marco.org/2015/01/04/apple-lost-functional-high-ground">Marco's post</a></li> <li><a href="http://www.marco.org/2015/01/05/popular-for-a-day">Marco's retrospective</a></li> <li><a href="http://video.cnbc.com/gallery/?video=3000343764">Mention on CNBC</a></li> <li><a href="http://5by5.tv/hypercritical/55">Hypercritical #55</a></li> <li><a href="http://www.caseyliss.com/2015/1/5/bravery">Casey's response to Marco</a></li> <li><a href="http://glog.glennf.com/blog/2015/1/6/the-software-and-services-apple-needs-to-fix">Glenn Fleishman's list</a></li></ul></li> <li>How to write for understanding <ul><li><a href="http://www.marco.org/2013/12/29/apple-doesnt-have-time">Marco laments about software quality in the past</a></li></ul></li> <li><a href="http://9to5mac.com/2015/01/06/macbook-air-12-inch-redesign/">Rumored 12" MacBook Air</a> <ul><li><a href="https://www.twelvesouth.com/product/plugbug">PlugBug</a></li> <li><a href="https://twitter.com/chockenberry/status/552928449250078721">Chockenberry on a potential ARM transition</a></li> <li><a href="https://en.wikipedia.org/wiki/Fat_binary">Fat binary</a></li> <li>Special thanks to <a href="http://david-smith.org/">_DavidSmith</a> for finding "bezels" in <a href="http://5by5.tv/hypercritical/22">Hypercritical #22</a></li></ul></li> </ul> <p>Sponsored by:</p> <ul> <li><a href="http://automatic.com/atp">Automatic</a>: Your smart driving assistant. Get $20 off with this link.</li> <li><a href="http://hover.com/atp">Hover</a>: The best way to buy and manage domain names. Use coupon code <strong>HIGHGROUND</strong> for 10% off.</li> <li><a href="https://caspersleep.com/atp">Casper</a>: A mattress with just the right sink, just the right bounce, for better nights and brighter days. Use code <strong>ATP</strong> for $50 off.</li> </ul>",
  "summary": null,
  "url": "http://atp.fm/episodes/99",
  "published": "2015-01-09T20:11:41.000000Z",
  "created_at": "2015-01-09T23:54:57.672303Z",
  "enclosure": {
    "enclosure_type": "audio/mpeg",
    "enclosure_url": "http://traffic.libsyn.com/atpfm/atp99.mp3",
    "enclosure_length": "86528647",
    "itunes_duration": "02:00:00"
  }
}
```
