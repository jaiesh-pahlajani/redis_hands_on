- Sorted Sets Commands 

ZADD myzset 2 "two" 3 "three" (https://redis.io/commands/zadd  Refer this link to know more.)

ZRANGE myzset 0 -1 WITHSCORES (Returns the specified range of elements in the sorted set stored at key.)

ZCARD myzset (Returns the sorted set cardinality (number of elements) of the sorted set stored at key.)


ZREM myzset "two" (Removes the specified members from the sorted set stored at key. Non existing members are ignored.)

ZSCORE myzset "one" (Returns the score of member in the sorted set at key.)

ZREVRANGE myzset 0 -1 (Returns the specified range of elements in the sorted set stored at key. The elements are considered to be ordered from the highest to the lowest score.)

ZRANK myzset "three" (Returns the rank of member in the sorted set stored at key, with the scores ordered from low to high. The rank (or index) is 0-based, which means that the member with the lowest score has rank 0.)

ZREVRANK myzset "one" (Returns the rank of member in the sorted set stored at key, with the scores ordered from high to low. The rank (or index) is 0-based, which means that the member with the highest score has rank 0.)

ZINCRBY myzset 2 "one" (Increments the score of member in the sorted set stored at key by increment.)

ZCOUNT myzset -inf +inf (Returns the number of elements in the sorted set at key with a score between min and max.)

ZPOPMAX myzset (Removes and returns up to count members with the highest scores in the sorted set stored at key.)

ZPOPMIN myzset (Removes and returns up to count members with the lowest scores in the sorted set stored at key.

ZINTERSTORE out 2 zset1 zset2 WEIGHTS 2 3 (Computes the intersection of numkeys sorted sets given by the specified keys, and stores the result in destination. )

ZUNIONSTORE out 2 zset1 zset2 WEIGHTS 2 3 (Computes the union of numkeys sorted sets given by the specified keys, and stores the result in destination.)

ZRANGEBYSCORE myzset (1 2 (Returns all the elements in the sorted set at key with a score between min and max)

ZRANGEBYLEX myzset - [c (https://redis.io/commands/zrangebylex Refer to this link to know more)

ZLEXCOUNT myzset [b [f (When all the elements in a sorted set are inserted with the same score, in order to force lexicographical ordering, this command returns the number of elements in the sorted set at key with a value between min and max.)

ZREVRANGEBYLEX myzset [c – (Apart from the reversed ordering, ZREVRANGEBYLEX is similar to ZRANGEBYLEX.)

ZREMRANGEBYLEX myzset [alpha [omega  (When all the elements in a sorted set are inserted with the same score, in order to force lexicographical ordering, this command removes all elements in the sorted set stored at key between the lexicographical range specified by min and max.)

ZREMRANGEBYRANK myzset 0 1 (Removes all elements in the sorted set stored at key with rank between start and stop.)

ZREMRANGEBYSCORE myzset -inf (2  (Removes all elements in the sorted set stored at key with a score between min and max (inclusive).)

ZREVRANGEBYSCORE myzset 2 (1  (Apart from the reversed ordering, ZREVRANGEBYSCORE is similar to ZRANGEBYSCORE.)


Examples - 

127.0.0.1:6379> zadd students 1 Jaiesh 2 Bob 3 Rob
(integer) 3

127.0.0.1:6379> zrange students 0 -1
1) "Jaiesh"
2) "Bob"
3) "Rob"

127.0.0.1:6379> zrange students 0 -1 WITHSCORES
1) "Jaiesh"
2) "1"
3) "Bob"
4) "2"
5) "Rob"
6) "3"
127.0.0.1:6379> zadd students 4 Shradz
(integer) 1

127.0.0.1:6379> zadd students 5 Shradz
(integer) 0

127.0.0.1:6379> zrange students 0 -1
1) "Jaiesh"
2) "Bob"
3) "Rob"
4) "Shradz"

127.0.0.1:6379> zadd students nx 5 Shradz
(integer) 0

127.0.0.1:6379> zrange students 0 -1
1) "Jaiesh"
2) "Bob"
3) "Rob"
4) "Shradz"

127.0.0.1:6379> zadd students 5 Shradz
(integer) 0

127.0.0.1:6379> zadd students nx 5 Shradzzz
(integer) 1

127.0.0.1:6379> zrange students 0 -1
1) "Jaiesh"
2) "Bob"
3) "Rob"
4) "Shradz"
5) "Shradzzz"

127.0.0.1:6379> zadd students nx 5 lolz
(integer) 1

127.0.0.1:6379> zrange students 0 -1
1) "Jaiesh"
2) "Bob"
3) "Rob"
4) "Shradz"
5) "Shradzzz"
6) "lolz"

127.0.0.1:6379> zadd students 5 lolz
(integer) 0

127.0.0.1:6379> zrange students 0 -1
1) "Jaiesh"
2) "Bob"
3) "Rob"
4) "Shradz"
5) "Shradzzz"
6) "lolz"

127.0.0.1:6379> zadd students 5 close
(integer) 1

127.0.0.1:6379> zrange students 0 -1
1) "Jaiesh"
2) "Bob"
3) "Rob"
4) "Shradz"
5) "Shradzzz"
6) "close"
7) "lolz"

127.0.0.1:6379> zrange students 0 -1 withscores
 1) "Jaiesh"
 2) "1"
 3) "Bob"
 4) "2"
 5) "Rob"
 6) "3"
 7) "Shradz"
 8) "5"
 9) "Shradzzz"
10) "5"
11) "close"
12) "5"
13) "lolz"
14) "5"

127.0.0.1:6379> zadd students 5 virat
(integer) 1

127.0.0.1:6379> zrange students 0 -1 withscores
 1) "Jaiesh"
 2) "1"
 3) "Bob"
 4) "2"
 5) "Rob"
 6) "3"
 7) "Shradz"
 8) "5"
 9) "Shradzzz"
10) "5"
11) "close"
12) "5"
13) "lolz"
14) "5"
15) "virat"
16) "5"

127.0.0.1:6379> zadd students ch 0 janss 10 rachael
(integer) 2

127.0.0.1:6379> zrange students 0 -1
 1) "janss"
 2) "Jaiesh"
 3) "Bob"
 4) "Rob"
 5) "Shradz"
 6) "Shradzzz"
 7) "close"
 8) "lolz"
 9) "virat"
10) "rachael"

127.0.0.1:6379> zrange students 0 -1 withscores
 1) "janss"
 2) "0"
 3) "Jaiesh"
 4) "1"
 5) "Bob"
 6) "2"
 7) "Rob"
 8) "3"
 9) "Shradz"
10) "5"
11) "Shradzzz"
12) "5"
13) "close"
14) "5"
15) "lolz"
16) "5"
17) "virat"
18) "5"
19) "rachael"
20) "10"

127.0.0.1:6379> zadd students incr 1 Jaiesh
"2"

127.0.0.1:6379> zrange students 0 -1 withscores
 1) "janss"
 2) "0"
 3) "Bob"
 4) "2"
 5) "Jaiesh"
 6) "2"
 7) "Rob"
 8) "3"
 9) "Shradz"
10) "5"
11) "Shradzzz"
12) "5"
13) "close"
14) "5"
15) "lolz"
16) "5"
17) "virat"
18) "5"
19) "rachael"
20) "10"

127.0.0.1:6379> zcard students
(integer) 10

127.0.0.1:6379> zrem students close
(integer) 1

127.0.0.1:6379> zrem students close Shradz Rob
(integer) 2

127.0.0.1:6379> zscore students Jaiesh
"2"

127.0.0.1:6379> zrevrange students 0 -1 
1) "rachael"
2) "virat"
3) "lolz"
4) "Shradzzz"
5) "Jaiesh"
6) "Bob"
7) "janss"

127.0.0.1:6379> zrank students virat
(integer) 5

127.0.0.1:6379> zrevrank students virat
(integer) 1

127.0.0.1:6379> zincrby studnets 3 virat
"3"

127.0.0.1:6379> zrange students 0 -1 withscores
 1) "janss"
 2) "0"
 3) "Bob"
 4) "2"
 5) "Jaiesh"
 6) "2"
 7) "Shradzzz"
 8) "5"
 9) "lolz"
10) "5"
11) "virat"
12) "5"
13) "rachael"
14) "10"

127.0.0.1:6379> zincrby students 3 virat
"8"

127.0.0.1:6379> zrange students 0 -1 withscores
 1) "janss"
 2) "0"
 3) "Bob"
 4) "2"
 5) "Jaiesh"
 6) "2"
 7) "Shradzzz"
 8) "5"
 9) "lolz"
10) "5"
11) "virat"
12) "8"
13) "rachael"
14) "10"

127.0.0.1:6379> zcount students 0 3
(integer) 3

127.0.0.1:6379> zcount students -inf +inf
(integer) 7

127.0.0.1:6379> zpopmax students 2
1) "rachael"
2) "10"
3) "virat"
4) "8"

127.0.0.1:6379> zrange students 0 -1 withscores
 1) "janss"
 2) "0"
 3) "Bob"
 4) "2"
 5) "Jaiesh"
 6) "2"
 7) "Shradzzz"
 8) "5"
 9) "lolz"
10) "5"

127.0.0.1:6379> zadd students 7 James
(integer) 1

127.0.0.1:6379> zpopmax students 1
1) "James"
2) "7"

127.0.0.1:6379> zpopmin students 2
1) "janss"
2) "0"
3) "Bob"
4) "2"

127.0.0.1:6379> zrange students 0 -1 withscores
1) "Jaiesh"
2) "2"
3) "Shradzzz"
4) "5"
5) "lolz"
6) "5"

127.0.0.1:6379> zadd z1 1 hey 2 hello
(integer) 2

127.0.0.1:6379> zadd z1 1 holla 3 hello
(integer) 1

127.0.0.1:6379> zadd z2 1 holla 3 hello
(integer) 2

127.0.0.1:6379> zrange z1 0 -1 
1) "hey"
2) "holla"
3) "hello"

127.0.0.1:6379> zrange z2 0 -1
1) "holla"
2) "hello"

127.0.0.1:6379> zrem z1 holla
(integer) 1

127.0.0.1:6379> zinterstore z3 2 z1 z2 weights 5 6 aggregate sum
(integer) 1

127.0.0.1:6379> zrange z3 0 -1 withscores
1) "hello"
2) "33"

127.0.0.1:6379> zinterstore z4 2 z1 z2 weights 5 6 aggregate max
(integer) 1

127.0.0.1:6379> zrange z4 0 -1 withscores
1) "hello"
2) "18"

127.0.0.1:6379> zinterstore z5 2 z1 z2 weights 5 6 aggregate min
(integer) 1

127.0.0.1:6379> zrange z5 0 -1 withscores
1) "hello"
2) "15"

127.0.0.1:6379> zunionstore z6 2 z1 z2 weights 5 6 aggregate min
(integer) 3

127.0.0.1:6379> zrange z6 0 -1 withscores
1) "hey"
2) "5"
3) "holla"
4) "6"
5) "hello"
6) "15"

127.0.0.1:6379> zunionstore z7 2 z1 z2 weights 5 6 aggregate max
(integer) 3

127.0.0.1:6379> zrange z7 0 -1 withscores
1) "hey"
2) "5"
3) "holla"
4) "6"
5) "hello"
6) "18"

127.0.0.1:6379> zunionstore z8 2 z1 z2 weights 5 6 aggregate sum
(integer) 3

127.0.0.1:6379> zrange z8 0 -1 withscores
1) "hey"
2) "5"
3) "holla"
4) "6"
5) "hello"
6) "33"

127.0.0.1:6379> zunionstore z9 2 z1 z2
(integer) 3

127.0.0.1:6379> zrange z9 0 -1 withscores
1) "hey"
2) "1"
3) "holla"
4) "1"
5) "hello"
6) "6"

127.0.0.1:6379> zrangebyscore students 0 5
1) "Jaiesh"
2) "Shradzzz"
3) "lolz"

127.0.0.1:6379> zrangebyscore students 0 5 withscores
1) "Jaiesh"
2) "2"
3) "Shradzzz"
4) "5"
5) "lolz"
6) "5"

127.0.0.1:6379> zrangebyscore students 0 5 withscores limit 1 2
1) "Shradzzz"
2) "5"
3) "lolz"
4) "5"

127.0.0.1:6379> zrangebylex students - +
1) "Jaiesh"
2) "Shradzzz"
3) "lolz"

127.0.0.1:6379> zadd students 0 Mahi
(integer) 1

127.0.0.1:6379> zrangebylex students - +
1) "Mahi"
2) "Jaiesh"
3) "Shradzzz"
4) "lolz"

127.0.0.1:6379> zrangebylex students (Mahi (Shradzz
(empty array)

127.0.0.1:6379> zrangebylex students (Mahi (Jaiesh
(empty array)

127.0.0.1:6379> zrangebylex students (Jaiesh (Shradzzz
1) "Mahi"
2) "Jaiesh"

127.0.0.1:6379> zrangebylex students [Jaiesh [Shradzzz
1) "Mahi"
2) "Jaiesh"
3) "Shradzzz"

127.0.0.1:6379> zlexcount students [Jaiesh [Shradzzz
(integer) 3

127.0.0.1:6379> zrevrangebylex students [Jaiesh [Shradzzz
(empty array)

127.0.0.1:6379> zrevrangebylex students (Jaiesh (Shradzzz
(empty array)

127.0.0.1:6379> zrevrangebylex students (Shradzz (Jaiesh
(empty array)

127.0.0.1:6379> zrevrangebylex students (Shradzzz (Jaiesh
(empty array)

127.0.0.1:6379> zrevrangebylex students (Shradzzz (Mahi
(empty array)

127.0.0.1:6379> zrevrangebylex students [Shradzzz [Mahi
1) "Shradzzz"

127.0.0.1:6379> zremrangebyrank students 0 1
(integer) 2

127.0.0.1:6379> zrange students 0 -1 withscores
1) "Shradzzz"
2) "5"
3) "lolz"
4) "5"

127.0.0.1:6379> zremrangebyscore students 5 6
(integer) 2

127.0.0.1:6379> zrange students 0 -1
(empty array)
