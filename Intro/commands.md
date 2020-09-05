- Basic commands

· Set Key value (returns OK)

· Get Key (returns the value or nil)

· DEL key1 key2 key3 (To delete a key). (returns number of keys deleted)

· EXISTS key1 key2 (To check a key exist or not). (returns count of keys available)

· TTL key  (To check time to live). (returns time in seconds, -1 if cannot expire, -2 if expired)

· EXPIRE key 10(in seconds). (returns 1)

· PTTL mykey (to check time in millisecond). (same as TTL)

· PEXPIRE mykey 1500 (Time in Milliseconds). (same as EXPIRE)

· PERSIST mykey (Remove EXPIRATION from the key) 

· KEYS a?? (Returns all keys matching pattern)

· RANDOMKEY (Return a random key from the currently selected database)

· RENAME mykey myotherkey

· RENAMENX mykey myotherkey (Renames key to newkey if newkey does not yet exist)

· TOUCH key1 key2 (Alters the last access time of a key(s).

· UNLINK key1 key2 key3 (The actual removal will happen later asynchronously.)

· TYPE key1 (Return Type of Value)

· DUMP mykey (Serialize the value stored at key in a Redis-specific format)

· RESTORE mykey 0 "\n\x17\x17\x00\x00\x00\x12\x00\x00\x00\x03\x00\”


- Examples

127.0.0.1:6379> set 1 hello
OK
127.0.0.1:6379> get 1
"hello"
127.0.0.1:6379> set name diwakar
OK
127.0.0.1:6379> get name
"diwakar"
127.0.0.1:6379> del 1
(integer) 1
127.0.0.1:6379> get 1
(nil)
127.0.0.1:6379> set 1 jello
OK
127.0.0.1:6379> set 2 lolwa
OK
127.0.0.1:6379> del 1 2
(integer) 2
127.0.0.1:6379> get 1 
(nil)
127.0.0.1:6379> del 1 2 3
(integer) 0
127.0.0.1:6379> exists 1
(integer) 0
127.0.0.1:6379> exists name
(integer) 1
127.0.0.1:6379> exists 1 name
(integer) 1
127.0.0.1:6379> exists 1
(integer) 0
127.0.0.1:6379> set jaiesh hello ex 10
OK
127.0.0.1:6379> ttl jaiesh
(integer) 5
127.0.0.1:6379> ttl jaiesh
(integer) -2
127.0.0.1:6379> get jaiesh
(nil)
127.0.0.1:6379> ttl 6
(integer) -2
127.0.0.1:6379> ttl name
(integer) -1
127.0.0.1:6379> set alexa 1
OK
127.0.0.1:6379> expire alexa 4
(integer) 1
127.0.0.1:6379> set alexa 90
OK
127.0.0.1:6379> pttl alexa 
(integer) -1
127.0.0.1:6379> expire alexa 4
(integer) 1
127.0.0.1:6379> pttl alexa 
(integer) 2006
127.0.0.1:6379> pexpire alexa 10000
(integer) 0
127.0.0.1:6379> pttl alexa
(integer) -2
127.0.0.1:6379> ttl aleza
(integer) -2
127.0.0.1:6379> ttl alexa
(integer) -2
127.0.0.1:6379> expire alexa 4
(integer) 0
127.0.0.1:6379> pexpire alexa 10000
(integer) 0
127.0.0.1:6379> pttl alexa
(integer) -2
127.0.0.1:6379> set kid 3
OK
127.0.0.1:6379> pexpire kid 90000
(integer) 1
127.0.0.1:6379> pttl kid
(integer) 83881
127.0.0.1:6379> pttl kid
(integer) 31187
127.0.0.1:6379> persist kid
(integer) 1
127.0.0.1:6379> ttl kid
(integer) -1
127.0.0.1:6379> clear

127.0.0.1:6379> set hello 1
OK
127.0.0.1:6379> get hello
"1"
127.0.0.1:6379> set hallo 2
OK
127.0.0.1:6379> set hrllo 3
OK
127.0.0.1:6379> set heello 2
OK
127.0.0.1:6379> set hijllo 2
OK
127.0.0.1:6379> keys h?llo
1) "hrllo"
2) "hello"
3) "hallo"
127.0.0.1:6379> keys *
1) "hrllo"
2) "kid"
3) "hello"
4) "hijllo"
5) "heello"
6) "name"
7) "hallo"
127.0.0.1:6379> keys h*llo
1) "hrllo"
2) "hello"
3) "hijllo"
4) "heello"
5) "hallo"
127.0.0.1:6379> keys h[ae]llo
1) "hello"
2) "hallo"
127.0.0.1:6379> keys h[ee]llo
1) "hello"
127.0.0.1:6379> keys h[ee][ee]llo
1) "heello"
127.0.0.1:6379> keys h[^e]llo
1) "hrllo"
2) "hallo"
127.0.0.1:6379> keys h[e-r]llo
1) "hrllo"
2) "hello"
127.0.0.1:6379> keys *ll*
1) "hrllo"
2) "hello"
3) "hijllo"
4) "heello"
5) "hallo"
127.0.0.1:6379> keys h????
1) "hrllo"
2) "hello"
3) "hallo"
127.0.0.1:6379> shutdown save
jaiesh@Jaieshs src % redis-cli
127.0.0.1:6379> get hello
"1"
127.0.0.1:6379> shutdown nosave
not connected> exit
jaiesh@Jaieshs src % get gello
zsh: command not found: get
jaiesh@Jaieshs src % redis-cli
127.0.0.1:6379> get hello
"1"
127.0.0.1:6379> shutdown nosave
not connected> exit
jaiesh@Jaieshs src % redis-cli
127.0.0.1:6379> Randomkey
"hello"
127.0.0.1:6379> keys
(error) ERR wrong number of arguments for 'keys' command
127.0.0.1:6379> keys *
1) "name"
2) "hello"
3) "kid"
4) "hrllo"
5) "hijllo"
6) "heello"
7) "hallo"
127.0.0.1:6379> Randomkey
"hallo"
127.0.0.1:6379> Randomkey
"heello"
127.0.0.1:6379> Rename hello 1
OK
127.0.0.1:6379> get 1
"1"
127.0.0.1:6379> get hello
(nil)
127.0.0.1:6379> randomkey
"name"
127.0.0.1:6379> set 1 yolo
OK
127.0.0.1:6379> set 2 mofo
OK
127.0.0.1:6379> rename 1 2
OK
127.0.0.1:6379> get 2
"yolo"
127.0.0.1:6379> set 3 kolo
OK
127.0.0.1:6379> rename 3 2
OK
127.0.0.1:6379> get 2
"kolo"
127.0.0.1:6379> get 2
"kolo"
127.0.0.1:6379> get 3
(nil)
127.0.0.1:6379> set 3 hahaha
OK
127.0.0.1:6379> renamenx 3 2
(integer) 0
127.0.0.1:6379> get 3
"hahaha"
127.0.0.1:6379> get 2
"kolo"
127.0.0.1:6379> renamenx 3 dudewa
(integer) 1
127.0.0.1:6379> get 3
(nil)
127.0.0.1:6379> get dudwa
(nil)
127.0.0.1:6379> touch dudewa
(integer) 1
127.0.0.1:6379> unlink dudwa
(integer) 0
127.0.0.1:6379> get dudewa
"hahaha"
127.0.0.1:6379> unlink dudwa
(integer) 0
127.0.0.1:6379> unlink dudewa
(integer) 1
127.0.0.1:6379> get dudewa
(nil)
127.0.0.1:6379> type 1
none
127.0.0.1:6379> type 2
string
127.0.0.1:6379> clear

127.0.0.1:6379> set hooli 3
OK
127.0.0.1:6379> dump hooli
"\x00\xc0\x03\t\x00\xe1h\xa1\xbe\x85\x03\x0f\x8e"
127.0.0.1:6379> restore hooli 0 "\x00\xc0\x03\t\x00\xe1h\xa1\xbe\x85\x03\x0f\x8e"
(error) BUSYKEY Target key name already exists.
127.0.0.1:6379> restore hooli 0 "\x00\xc0\x03\t\x00\xe1h\xa1\xbe\x85\x03\x0f\x8e" REPLACE
OK
127.0.0.1:6379> del hoolo
(integer) 0
127.0.0.1:6379> del hooli
(integer) 1
127.0.0.1:6379> restore hooli 0 "\x00\xc0\x03\t\x00\xe1h\xa1\xbe\x85\x03\x0f\x8e"
OK
127.0.0.1:6379> get hooli
"3"
