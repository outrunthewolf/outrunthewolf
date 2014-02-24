---
layout: entry
title: Redis with MySQL
---

I've recently been working on a large project, a very interesting API. One of the goals of the project was to build a learning spell/grammar checker.

There are lots of third party applications that can spell and grammar check, but not many that are free, offer a self-hosted solution and learn. By learn I mean present a user or set of users with spell/grammar suggestions and learn from their choices, so in future they and everyone else get better results.

### State of affairs
Our first in house tests were based around a simple MySQL database coupled with the spelling grammar API's. We sent back suggestions, and updated mysql with the complex learning data, very simple, but also quite slow.
Performing tests on the data it was easy to see that with large amounts of incoming data would not scale easily, synchrounous writes on learning feedback are slowing down user request receipts, and impacting performance for others.

### Middleground
We'd already discussed Memcache as a way of speeding up outgoing results from the off-start. And of course, it was great, but we're still writing data back to the database during an incoming request, we're also then pulling complex learning data back on top of that. We could easily write the data back to Memcache instead of the database and parse it out seperately during off peak times, but Memcache is not a persistant store, and if we encountered any issues, we could permamnently lose a good proportion of data.

### Solutions
What we ideally wanted was an easy way to write and read to memory, whilst maintaining a high amount of persistance and utilising a simple API. In stepped Redis.

We instituted a "no direct reads/writes" rule for the SQL backend. What this means is everything goes through redis. Any data we want to update in the SQL database is updated in Redis first, that is so the cache is instantly available with any changes without us having to "re-hydrate" it. Then any new requests that come in will contain the updated data immediately.

Now I'm all up for dropping the SQL database and working directly from Redis, but people are still a little nervous about losing something as solid as an SQL database for something new like Redis, we also need to consider the fact that for some reason Redis could fail. This leaves us with the small issue of maintaining the SQL database in sync with Redis.

We've analysed a few approaches, using publish methods from Redis to make asynchronous transacions, PHP cronjobs reading data back and forth. The apporach we've taken is to use Python to read the RDB dump files directly from the disk, parse them into JSON, and insert the data into MYSQL.

We used the fantastic [RDB Tools](https://github.com/sripathikrishnan/redis-rdb-tools "RDB Tools") 