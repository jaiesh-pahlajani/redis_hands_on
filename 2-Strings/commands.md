- Commands

· APPEND mykey "Hello" (appends the value at the end of the string).

· INCR mykey (Increments the number stored at key by one).

· INCRBY mykey 5

· DECR mykey (Decrements the number stored at key by one.)

· DECRBY mykey 3 (Decrements the number stored at key )

· INCRBYFLOAT mykey 0.1(Increment the string representing a floating point number)

· GETSET mycounter "0" (Atomically sets key to value and returns the old value stored at key)

· MSET key1 "Hello" key2 "World" (Sets the given keys to their respective values.)

· MGET key1 key2 (Returns the values of all specified keys).

· SETNX mykey "Hello" (Set key to hold string value if key does not exist.)

· MSETNX key1 "Hello" key2 "there" (Sets the given keys to their respective values.)

· GETRANGE mykey 0 3 (Returns the substring of the string value stored at key).

· GETRANGE mykey -3 -1. (-1 means the last character and so on).

· SETEX mykey 10 "Hello" (Set key to hold the string value and set key to timeout after a given number of seconds.)

· PSETEX mykey 1000 "Hello" ( expire time is specified in milliseconds instead of seconds.)

· SETRANGE key1 6 "Redis" (Overwrites part of the string stored at key) .

· STRLEN mykey (Returns the length of the string).


- Examples 

127.0.0.1:6379> set 1 abc
OK

127.0.0.1:6379> type 1
string

127.0.0.1:6379> set 2 "hello"
OK

127.0.0.1:6379> set 2 "lol" NX
(nil)

127.0.0.1:6379> keys *
1) "hrllo"
2) "heello"
3) "hooli"
4) "name"
5) "hallo"
6) "hijllo"
7) "kid"
8) "2"
9) "1"

127.0.0.1:6379> set 4 hello
OK

127.0.0.1:6379> set 5 hello nx
OK

127.0.0.1:6379> set 5 hey xx
OK

127.0.0.1:6379> set 10 hey xx
(nil)

127.0.0.1:6379> set greeting hello
OK

127.0.0.1:6379> append greeting world
(integer) 10

127.0.0.1:6379> get greeting
"helloworld"

127.0.0.1:6379> set score 1
OK

127.0.0.1:6379> incr score
(integer) 2

127.0.0.1:6379> type score
string

127.0.0.1:6379> incr score
(integer) 3

127.0.0.1:6379> decr score
(integer) 2

127.0.0.1:6379> incrby score 5
(integer) 7

127.0.0.1:6379> decrby score 2
(integer) 5

127.0.0.1:6379> set num 1.0
OK

127.0.0.1:6379> type num
string

127.0.0.1:6379> incrbyfloat num 2.3
"3.3"

127.0.0.1:6379> set 1 hello
OK

127.0.0.1:6379> getset 1 bye
"hello"

127.0.0.1:6379> get 1
"bye"

127.0.0.1:6379> getset wwe yolo
(nil)

127.0.0.1:6379> get wwe
"yolo"

127.0.0.1:6379> mset 1 h 2 g 3 e
OK

127.0.0.1:6379> keys *
 1) "wwe"
 2) "greeting"
 3) "5"
 4) "3"
 5) "4"
 6) "hrllo"
 7) "heello"
 8) "hooli"
 9) "name"
10) "score"
11) "hallo"
12) "hijllo"
13) "num"
14) "kid"
15) "2"
16) "1"

127.0.0.1:6379> mget 1 2 3
1) "h"
2) "g"
3) "e"

127.0.0.1:6379> msetnx 1 hey 2 hey 78 gg
(integer) 0

127.0.0.1:6379> msetnx 80 hey 90 hey 78 gg
(integer) 1

127.0.0.1:6379> set name samsung
OK

127.0.0.1:6379> getrange name 0 3
"sams"

127.0.0.1:6379> getrange name 3 4
"su"

127.0.0.1:6379> getrange name 0 -1
"samsung"

127.0.0.1:6379> getrange name 0 -2
"samsun"

127.0.0.1:6379> getrange name -1 -4
""

127.0.0.1:6379> getrange name -3 -2
"un"

127.0.0.1:6379> setex a 5 hello
OK

127.0.0.1:6379> keys *
 1) "hrllo"
 2) "3"
 3) "name"
 4) "hijllo"
 5) "score"
 6) "kid"
 7) "2"
 8) "1"
 9) "80"
10) "wwe"
11) "greeting"
12) "5"
13) "4"
14) "78"
15) "heello"
16) "hooli"
17) "hallo"
18) "num"
19) "90"

127.0.0.1:6379> setex a 5 hello
OK

127.0.0.1:6379> keys *
 1) "hrllo"
 2) "3"
 3) "name"
 4) "hijllo"
 5) "score"
 6) "kid"
 7) "2"
 8) "1"
 9) "80"
10) "wwe"
11) "greeting"
12) "5"
13) "4"
14) "78"
15) "heello"
16) "hooli"
17) "hallo"
18) "num"
19) "90"
20) "a"

127.0.0.1:6379> keys *
 1) "hrllo"
 2) "3"
 3) "name"
 4) "hijllo"
 5) "score"
 6) "kid"
 7) "2"
 8) "1"
 9) "80"
10) "wwe"
11) "greeting"
12) "5"
13) "4"
14) "78"
15) "heello"
16) "hooli"
17) "hallo"
18) "num"
19) "90"
20) "a"

127.0.0.1:6379> keys *
 1) "hrllo"
 2) "3"
 3) "name"
 4) "hijllo"
 5) "score"
 6) "kid"
 7) "2"
 8) "1"
 9) "80"
10) "wwe"
11) "greeting"
12) "5"
13) "4"
14) "78"
15) "heello"
16) "hooli"
17) "hallo"
18) "num"
19) "90"

127.0.0.1:6379> psetex a 123123 hello
OK

127.0.0.1:6379> get a
"hello"

127.0.0.1:6379> get a
"hello"

127.0.0.1:6379> pttl a
(integer) 113909

127.0.0.1:6379> ttl a
(integer) 111

127.0.0.1:6379> set k1 helloworld
OK

127.0.0.1:6379> set k1 "hello world"
OK

127.0.0.1:6379> setrange k1 6 redis
(integer) 11

127.0.0.1:6379> get k1
"hello redis"

127.0.0.1:6379> setrange k1 6 jai
(integer) 11

127.0.0.1:6379> get k1
"hello jaiis"

127.0.0.1:6379> strlen k1
(integer) 11
