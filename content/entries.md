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

| Parameter          | Required | Example                                                                                                             |
| ------------------ | -------- | ------------------------------------------------------------------------------------------------------------------- |
| `page: number`     | false    | `GET /v2/entries.json?page=2`  will get page two of the available entries                                           |
| `since: date`      | false    | `GET /v2/entries.json?since=2013-02-02T14:07:33.000000Z` will get all entries created after the iso 8601 timestamp. |
| `read: boolean`    | false    | `GET /v2/entries.json?read=false`  will get all unread entries.                                                     |
| `starred: boolean` | false    | `GET /v2/entries.json?starred=true`  will get all starred entries.                                                  |
| `ids: number(s)`   | false    | `GET /v2/entries.json?ids=1,2,3`  will get the entries with the ids 1, 2 and 3.                                     |


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

Supports the same parameters as `/v2/entries.json`

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
