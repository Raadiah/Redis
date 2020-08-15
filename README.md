# Redis
This is an open source documentation and work done under **Brilliant Cloud Research Team**. The goal of this sub-project is:
* Understanding core concepts of redis
* Implement a Redis cluster that will hold data of millions
* Document all work

So, let's start with Redis! 

## A simple illustration of Redis
Redis is an in-memory data structure store. By in-memory we mean that Redis stays on main memory, that is RAM, which makes it super fast also. It can store several kind of data structures. These are: strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, geospatial indexes with radius queries and streams.

Now, here is the interesting part of Redis. It is not a relational database like MySQL or PostgreSQL etc. We do not save data in form of tables here. So how do we store the data? Data are stored in form of key-value pair. Here, values can be retrieved using the key, but the vice-versa is not possible. So,

```
SET KEY VALUE

```

sets value to a key. And,

```
GET KEY

```

gets value from a key!

#### Now, where is Redis used?

Redis has three kind of application. It can be used as:

* Database
* Cache
* Message broker
