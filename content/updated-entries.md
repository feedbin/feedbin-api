Updated Entries
===============

Updated entries are entries that have been modified after they were originally published.

Feedbin stores both the original version of an entry and the latest version.

On the web [Feedbin gives the user an option to show a diff of the original and the latest](http://blog.feedbin.com/2014/12/16/never-miss-an-update-with-the-new-updated-section/) which highlights what has changed.

Using this API
--------------

The updated entry API gives you a list of entry ids that have been updated. Once you know which ids to ask for you can use the `entries` API to get the actual changes:

1. `include_original`
1. `include_content_diff`

For example:

`GET /v2/entries.json?include_original=true&include_content_diff=true&ids=703369824`

```json
[
  {
    "id": 703369824,
    "feed_id": 47,
    "title": "The Talk Show: \u2018Malaprops\u2019",
    "author": "John Gruber",
    "content": "<p>New episode of my podcast, The Talk Show, with special guest <a href=\"http:\/\/stratechery.com\/\">Ben Thompson<\/a>. Topics include Apple\u2019s pseudo \u201csabbaticals\u201d (employees who leave the company but then return after a year or two); Google\u2019s cultural similarities to Microsoft; the ways that Apple (and iOS users) might miss Scott Forstall; accessibility as a high priority for Apple; Instagram\u2019s success (and how they effectively ate Hipstamatic\u2019s lunch); a debate on just how \u201csimple\u201d Twitter is; Box\u2019s successful IPO, and Dropbox\u2019s support for Yosemite\u2019s official Finder integration for such services; MIT economist Jonathan Gruber pissing in my Google juice; Chromebooks; Amazon\u2019s overall strategy, and the colossal failure of their Fire Phone; and, lastly, a good chunk on Microsoft\u2019s Windows 10\/HoloLens event last week.<\/p>\n\n<p>Brought to you by three excellent sponsors:<\/p>\n\n<ul>\n<li>\n<a href=\"http:\/\/fractureme.com\/\">Fracture<\/a>: Your pictures, printed directly on glass. Use code \u201cdaringfireball\u201d and save $5.<\/li>\n<li>\n<a href=\"https:\/\/neededition.com\/\">Need<\/a>: A refined retailer and lifestyle magazine for men.<\/li>\n<li>\n<a href=\"http:\/\/www.igloosoftware.com\/thetalkshow\">Igloo<\/a>: The intranet you\u2019ll actually like.<\/li>\n<\/ul>\n\n<p><strong>Update:<\/strong> <a href=\"https:\/\/twitter.com\/OvercastFM\/status\/559462801341964288\">Overcast users may need to unsubscribe\/resubscribe<\/a> to the show if this episode isn\u2019t appearing for you.<\/p>\n\n<div>\n<a title=\"Permanent link to \u2018The Talk Show: \u2018Malaprops\u2019\u2019\" href=\"http:\/\/daringfireball.net\/linked\/2015\/01\/26\/the-talk-show-108\">\u00a0\u2605\u00a0<\/a>\n<\/div>",
    "summary": null,
    "url": "http:\/\/daringfireball.net\/thetalkshow\/2015\/01\/24\/ep-108",
    "published": "2015-01-26T23:49:33.000000Z",
    "created_at": "2015-01-26T23:52:17.106111Z",
    "original": {
      "author": "John Gruber",
      "content": "<p>New episode of my podcast, The Talk Show, with special guest <a href=\"http:\/\/stratechery.com\/\">Ben Thompson<\/a>. Topics include Apple\u2019s pseudo \u201csabbaticals\u201d (employees who leave the company but then return after a year or two); Google\u2019s cultural similarities to Microsoft; the ways that Apple (and iOS users) might miss Scott Forstall; accessibility as a high priority for Apple; Instagram\u2019s success (and how they effectively ate Hipstamatic\u2019s lunch); a debate on just how \u201csimple\u201d Twitter is; Box\u2019s successful IPO, and Dropbox\u2019s support for Yosemite\u2019s official Finder integration for such services; MIT economist Jonathan Gruber pissing in my Google juice; Chromebooks; Amazon\u2019s overall strategy, and the colossal failure of their Fire Phone; and, lastly, a good chunk on Microsoft\u2019s Windows 10\/HoloLens event last week.<\/p>\n\n<p>Brought to you by three excellent sponsors:<\/p>\n\n<ul>\n<li><a href=\"http:\/\/fractureme.com\/\">Fracture<\/a>: Your pictures, printed directly on glass. Use code \u201cdaringfireball\u201d and save $5.<\/li>\n<li><a href=\"https:\/\/neededition.com\/\">Need<\/a>: A refined retailer and lifestyle magazine for men.<\/li>\n<li><a href=\"http:\/\/www.igloosoftware.com\/thetalkshow\">Igloo<\/a>: The intranet you\u2019ll actually like.<\/li>\n<\/ul>\n\n<div>\n<a  title=\"Permanent link to \u2018The Talk Show: &#8216;Malaprops&#8217;\u2019\"  href=\"http:\/\/daringfireball.net\/linked\/2015\/01\/26\/the-talk-show-108\">&nbsp;\u2605&nbsp;<\/a>\n<\/div>",
      "title": "The Talk Show: \u2018Malaprops\u2019",
      "url": "http:\/\/daringfireball.net\/thetalkshow\/2015\/01\/24\/ep-108",
      "entry_id": "tag:daringfireball.net,2015:\/linked\/\/6.30510",
      "published": "2015-01-26T23:49:33.000Z",
      "data": null
    },
    "content_diff": "<div class=\"inline-diff\"><p>New episode of my podcast, The Talk Show, with special guest <a href=\"http:\/\/stratechery.com\/\">Ben Thompson<\/a>. Topics include Apple\u2019s pseudo \u201csabbaticals\u201d (employees who leave the company but then return after a year or two); Google\u2019s cultural similarities to Microsoft; the ways that Apple (and iOS users) might miss Scott Forstall; accessibility as a high priority for Apple; Instagram\u2019s success (and how they effectively ate Hipstamatic\u2019s lunch); a debate on just how \u201csimple\u201d Twitter is; Box\u2019s successful IPO, and Dropbox\u2019s support for Yosemite\u2019s official Finder integration for such services; MIT economist Jonathan Gruber pissing in my Google juice; Chromebooks; Amazon\u2019s overall strategy, and the colossal failure of their Fire Phone; and, lastly, a good chunk on Microsoft\u2019s Windows 10\/HoloLens event last week.<\/p><p>Brought to you by three excellent sponsors:<\/p><ul>\n<li>\n<a href=\"http:\/\/fractureme.com\/\">Fracture<\/a>: Your pictures, printed directly on glass. Use code \u201cdaringfireball\u201d and save $5.<\/li>\n<li>\n<a href=\"https:\/\/neededition.com\/\">Need<\/a>: A refined retailer and lifestyle magazine for men.<\/li>\n<li>\n<a href=\"http:\/\/www.igloosoftware.com\/thetalkshow\">Igloo<\/a>: The intranet you\u2019ll actually like.<\/li>\n<\/ul><p class=\"diff-ins\"><strong>Update:<\/strong> <a href=\"https:\/\/twitter.com\/OvercastFM\/status\/559462801341964288\">Overcast users may need to unsubscribe\/resubscribe<\/a> to the show if this episode isn\u2019t appearing for you.<\/p><div>\n<a title=\"Permanent link to \u2018The Talk Show: \u2018Malaprops\u2019\u2019\" href=\"http:\/\/daringfireball.net\/linked\/2015\/01\/26\/the-talk-show-108\">\u00a0\u2605\u00a0<\/a>\n<\/div><\/div>"
  }
]
```

The `content_diff` is an HTML diff of the original and latest version. You can style this with CSS. [Here are the styles that Feedbin uses](https://github.com/feedbin/feedbin/blob/2610ba5aed103789d2a61708ffcd10d0432b5161/app/assets/stylesheets/_site.scss#L3246-L3309) so you know what to target.


Get Updated Entries
-------------------

 - `GET /v2/updated_entries.json` will return an array of entry_ids


```json
[4087,4088,4089,4090,4091,4092,4093,4094,4095,4096,4097]
```

| Parameter                       | Required | Example                                                                                                                                           |
| ------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `since: date`                   | false    | `GET /v2/updated_entries.json?since=2013-02-02T14:07:33.000000Z` will get all updated_entries updated after the iso 8601 timestamp.               |               |


**Status Codes**

- `200 OK` will be returned

**Note** The order of IDs is how

Delete Updated Entries (mark as read)
-------------------------------------

- `DELETE /v2/updated_entries.json` will mark the specified entry_ids as read.

**Request**

```json
{
  "updated_entries": [4089, 4090, 4091]
}
```

**Status Codes**

- `200 OK` will be returned if the request is successful

The response will contain all of the entry_ids that were successfully deleted.

**DELETE Alternative**

Some clients like Android don't easily allow a body with a DELETE request. For these cases there is an alternate endpoint that can be used with POST:

`POST /v2/updated_entries/delete.json`
