This is the documentation for version 1 of the Feedbin API.

Version 1 has been deprecated and will be turned off once all clients are able to switch over.

Version 1 has a design flaw with `entry_states` where Feedbin needs to store too much historical data to maintain these records.

Storing the records themselves is not an issue so much as the index/memory requirements that are needed to keep them performant.

API Objects
-----------

- [Subscriptions](subscriptions.md)
- [Feeds](feeds.md)
- [Entries](entries.md)
- [Entry States](entry-states.md)
- [Taggings](taggings.md)
