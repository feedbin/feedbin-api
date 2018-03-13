Supporting Twitter
==================

Feedbin [supports subscribing to Twitter](https://feedbin.com/blog/2018/01/11/feedbin-is-the-best-way-to-read-twitter/) as a data source. You don't have to do anything to support Twitter, but if you want to provide a tailored Twitter experience, Feedbin provides the data to help make that happen.

The Twitter terms of service do not allow their API data to be redistributed, but there is a straightforward way to get full tweet data.

1. Register your app on the [Twitter developer site](https://apps.twitter.com/).
1. Build a Twitter authentication flow in your app so you can get Twitter data on behalf of the user.
1. Use the `extended` mode when fetching entries from Feedbin to get the data necessary to load tweets.
1. Use Twitter's [`statuses/lookup` API](https://developer.twitter.com/en/docs/tweets/post-and-engage/api-reference/get-statuses-lookup) to bulk load tweets by ID.

### Getting Twitter IDs from Feedbin

Load entries using the extended mode. You'll get the `twitter_id` and `twitter_thread_ids` as well as the normal entry data. Then you can [load tweets by id](https://developer.twitter.com/en/docs/tweets/post-and-engage/api-reference/get-statuses-lookup), 100 at-a-time, from Twitter.

```
GET /v2/entries.json?mode=extended
```

```json
{
    "id": 1682191545,
    "feed_id": 1379740,
    ...
    "twitter_id": 973315765393920000,
    "twitter_thread_ids": [973315765393920000, 973315765393920001],
    "extracted_articles": []
}
```
