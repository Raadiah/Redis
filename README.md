# Redis
This is an open source documentation and work done as an assignment under **Brilliant Cloud Research Team**. The goal of this sub-project is:
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

## Example of use of Redis as a database

We have seen before that Redis stores value as a key-value pair. To understand, how Redis can be used as a database, we must look at some instructions and the data structures supported by Redis. Note that, not all are data structures are covered here.

### String

They are stored as key value pair as shown above.

```
SET name "Peter"
GET name => Peter

```

An interesting operation is `INCR` which parses the string value as an integer and increases it by 1. The operation is atomic.

### List

These are linked lists. You can push element to a list using ```LPUSH``` which pushes to the left of the list, or ```RPUSH``` which pushes to the right of the string.

```
LPUSH sample_list a
RPUSH sample_list b
LPUSH sample_list c

```

The resultant list of the above command will be a list like 

```
'c', 'a', 'b'
```
Now, range query of the list is possible. For example

```
LRANGE sample_list 0 1 => c, a
LRANGE sample_list 0 -1 => c, a, b
```
###### NOTES
1. Sample_list is the key here, and the whole list is the value
1. The index is zero based. 
1. In second command, a negative value is used. It has another meaning. -1 means last element. -2 means second last element and so on. So, 0 -1 means all elements from range 0 to last element.
1. We do not have to create empty list or remove a list when it is empty. It is the responsibility of Redis to remove the key when it is empty. In the example

### Set

These are unordered set. To add an element to the set:

```
SADD myset a
SADD myset b
SADD myset foo
SADD myset bar
SCARD myset => 4
SMEMBERS myset => bar,a,foo,b
```

### Redis Hashes

They  are field-value pair data structure. To set a  hash:

```
HMSET myuser name Peter sur_name Pan city Neverland
HGET myuser city => Neverland
```
In the [official documentation](https://redis.io/topics/data-types-intro) it says, *While hashes are handy to represent objects, actually the number of fields you can put inside a hash has no practical limits (other than available memory), so you can use hashes in many different ways inside your application.*

### Creating a database

Now, suppose you need a database of the schema: person. The description of the schema is:

  Person Schema | 
  ---------------------------------------------------------- | 
  Person Id | 
  National Id | 
  Name | 



Here, Person Id is auto increment. National Id is saved for unique person.

So you can use the following structure to create the database. Firstly, we initialize Person_id with 0.

``` 
SET Person_id 0
```

When a new person registers:

```
INCREMENT Person_id => 1
HMSET user:1 National_Id 6fYtthat Name Peter
HSET users 6fYtthat 1

```
Here, every time a new person is registered the *Person_id* is increased by 1. Then at the *user:person_id* the information of the person is saved. To keep a set of all the users a hash *users* is created which is populated with *National_Id* (which is "6fYtthat") refering to the *Person_id*. 

This is a common design pattern using key value data structure. That is how you make a database! Easy and fun, right?


