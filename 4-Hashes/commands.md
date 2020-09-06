- Commands

HSET myhash field1 "Hello".  (Sets field in the hash stored at key to value. If field already exists in the hash, it is overwritten.)

HGET myhash field1 (Returns the value associated with field in the hash stored at key.)

HMSET myhash field1 "Hello" field2 "World" ( Set Multiple values.)

HGETALL myhash  (Returns all fields and values of the hash stored at key.)

HMGET myhash field1 field2 (Returns the values associated with the specified fields in the hash stored at key.)

HEXISTS myhash field1 (Returns if field is an existing field in the hash stored at key.)

HKEYS myhash (Returns all field names in the hash stored at key.)

HLEN myhash (Returns the number of fields contained in the hash stored at key.)

HSETNX myhash field "Hello" (Sets field in the hash stored at key to value, only if field does not yet exist.)

HDEL myhash field1 (Removes the specified fields from the hash stored at key.)

HINCRBY myhash field 1 (Increments the number stored at field in the hash stored at key by increment.)

HINCRBYFLOAT mykey field 0.1 (Increment the specified field of a hash stored at key, and representing a floating-point number, by the specified increment.)

HSTRLEN myhash f1 (Returns the string length of the value associated with field in the hash stored at key.)

HVALS myhash (Returns all values in the hash stored at key.)


- Examples 

127.0.0.1:6379> hset student name jaiesh
(integer) 1

127.0.0.1:6379> hget student name 
"jaiesh"

127.0.0.1:6379> hset set age 23
(integer) 1

127.0.0.1:6379> hset set age 23
(integer) 0

127.0.0.1:6379> hset set name sachin
(integer) 1

127.0.0.1:6379> hset set name sachin
(integer) 0

127.0.0.1:6379> hmset player name virat age 34
OK

127.0.0.1:6379> hmget player name
1) "virat"

127.0.0.1:6379> hgetall player
1) "name"
2) "virat"
3) "age"
4) "34"

127.0.0.1:6379> hmget player name age
1) "virat"
2) "34"

127.0.0.1:6379> hmget player name age abcd
1) "virat"
2) "34"
3) (nil)

127.0.0.1:6379> hvals player
1) "virat"
2) "34"

127.0.0.1:6379> hkeys player
1) "name"
2) "age"

127.0.0.1:6379> hexists player name
(integer) 1

127.0.0.1:6379> hlen player
(integer) 2

127.0.0.1:6379> hset player hobby football
(integer) 1

127.0.0.1:6379> hset player hobby cricket
(integer) 0

127.0.0.1:6379> hsetnx player hobby cricket
(integer) 0

127.0.0.1:6379> hget player hobby
"cricket"

127.0.0.1:6379> hsetnx player hobby football
(integer) 0

127.0.0.1:6379> hget player hobby
"cricket"

127.0.0.1:6379> hdel player hobby
(integer) 1

127.0.0.1:6379> hgetall player
1) "name"
2) "virat"
3) "age"
4) "34"

127.0.0.1:6379> hincrby player age 2
(integer) 36

127.0.0.1:6379> hincrbyfloat player age 1.2
"37.2"

127.0.0.1:6379> hstrlen player name
(integer) 5
