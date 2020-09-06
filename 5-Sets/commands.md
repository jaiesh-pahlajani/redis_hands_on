- Commands

SADD myset "Hello" Add the specified members to the set stored at key.

SMEMBERS myset (Returns all the members of the set value stored at key.)

SISMEMBER myset "one” (Returns if member is a member of the set stored at key.)

SCARD myset(Returns the set cardinality (number of elements) of the set stored at key.)

SMOVE myset myotherset "two" (Move member from the set at source to the set at destination.)

SPOP myset (Removes and returns one or more random elements from the set value store at key.)

SREM myset "one" (Remove the specified members from the set stored at key.)

SDIFF key1 key (Returns the members of the set resulting from the difference between the first set and all the successive sets.)

SDIFFSTORE key key1 key2(This command is equal to SDIFF, but instead of returning the resulting set, it is stored in destination.)

SINTER key1 key2 (Returns the members of the set resulting from the intersection of all the given sets.)

SINTERSTORE key key1 key2(This command is equal to SINTER, but instead of returning the resulting set, it is stored in destination.)

SUNION key1 key2 (Returns the members of the set resulting from the union of all the given sets.)

SUNIONSTORE key key1 key2(This command is equal to SUNION, but instead of returning the resulting set, it is stored in destination.)

SRANDMEMBER myset 2 ( When called with just the key argument, return a random element from the set value stored at key.)


- Examples 

127.0.0.1:6379> sadd club messi ronaldo
(integer) 2

127.0.0.1:6379> smembers club
1) "ronaldo"
2) "messi"

127.0.0.1:6379> sadd club neymar
(integer) 1

127.0.0.1:6379> smembers club
1) "ronaldo"
2) "neymar"
3) "messi"

127.0.0.1:6379> sismember club messi
(integer) 1

127.0.0.1:6379> sismember club random
(integer) 0

127.0.0.1:6379> scard club
(integer) 3

127.0.0.1:6379> sadd club2 lampard rooney
(integer) 2

127.0.0.1:6379> smove club2 club messi
(integer) 0

127.0.0.1:6379> smove club club2 messi
(integer) 1

127.0.0.1:6379> smembers club
1) "ronaldo"
2) "neymar"

127.0.0.1:6379> smembers club2
1) "lampard"
2) "messi"
3) "rooney"

127.0.0.1:6379> smove club2 club abc
(integer) 0

127.0.0.1:6379> spop club2 2
1) "messi"
2) "lampard"

127.0.0.1:6379> srem club ronadlo
(integer) 0

127.0.0.1:6379> smembers club
1) "ronaldo"
2) "neymar"

127.0.0.1:6379> srem club ronaldo
(integer) 1

127.0.0.1:6379> smembers club
1) "neymar"

127.0.0.1:6379> sdiff club club2
1) "neymar"

127.0.0.1:6379> sadd club messi ronaldo lampard rooney
(integer) 4

127.0.0.1:6379> sadd club2 kaka fabregas messi lampart
(integer) 4

127.0.0.1:6379> sdiff club club2
1) "lampard"
2) "ronaldo"
3) "neymar"

127.0.0.1:6379> sdiff club2 club
1) "fabregas"
2) "lampart"
3) "kaka"

127.0.0.1:6379> sunion club club2
1) "ronaldo"
2) "neymar"
3) "fabregas"
4) "rooney"
5) "kaka"
6) "lampard"
7) "lampart"
8) "messi"

127.0.0.1:6379> sinter club club2
1) "rooney"
2) "messi"

127.0.0.1:6379> sdiffstore club3 club clubb2
(integer) 5

127.0.0.1:6379> smembers club3
1) "lampard"
2) "ronaldo"
3) "neymar"
4) "rooney"
5) "messi"

127.0.0.1:6379> sinterstore club4 club club2
(integer) 2

127.0.0.1:6379> smembers club4
1) "messi"
2) "rooney"

127.0.0.1:6379> sunionstore club5 club club2
(integer) 8

127.0.0.1:6379> smembers club5
1) "ronaldo"
2) "neymar"
3) "fabregas"
4) "rooney"
5) "kaka"
6) "lampard"
7) "lampart"
8) "messi"

127.0.0.1:6379> srandmember club
"ronaldo"

127.0.0.1:6379> srandmember club
"ronaldo"

127.0.0.1:6379> srandmember club
"rooney"

127.0.0.1:6379> del club5
(integer) 1
