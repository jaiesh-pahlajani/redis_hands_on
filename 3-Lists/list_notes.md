- Lists

Properties of a list implemented using an array are very different 
from properties of list using linked list.

Redis lists are implemented via linked lists.

Accessing via index is not that efficient as it is not implemented by array.

- Commands

RPUSH mylist "hello" (Insert all the specified values at the tail of the list stored at key.)

LRANGE mylist 0 -1 (Returns the specified elements of the list stored at key.)

LPUSH mylist "world" (Insert all the specified values at the head of the list stored at key.)

RPUSHX mylist "World" (Inserts value at the tail of the list stored at key, only if key already exists and holds a list.)

LPUSH mylist "World" (Inserts value at the head of the list stored at key, only if key already exists and holds a list.)

RPOP mylist (Removes and returns the last element of the list stored at key.)

LPOP mylist (Removes and returns the first element of the list stored at key.)

LTRIM mylist 1 -1 (Trim an existing list so that it will contain only the specified range of elements specified)

LSET mylist 0 "four" (Sets the list element at index to value.)

LINDEX mylist 0 (Returns the element at index in the list stored at key.)

LINSERT mylist BEFORE "World" "There" (Inserts value in the list stored at key either before or after the reference value pivot.)

LLEN mylist (Returns the length of the list stored at key. )

LREM mylist 2 "hello" (Removes the first count occurrences of elements equal to value from the list stored at key.)

Examples - 

127.0.0.1:6379> lpush fruit banana 
(integer) 1

127.0.0.1:6379> lpush fruit banana mango apple
(integer) 4

127.0.0.1:6379> lrange fruit  0 -1
1) "apple"
2) "mango"
3) "banana"
4) "banana"

127.0.0.1:6379> rpush fruit pineapple
(integer) 5

127.0.0.1:6379> lrange fruit 0 -1
1) "apple"
2) "mango"
3) "banana"
4) "banana"
5) "pineapple"

127.0.0.1:6379> lrange fruit 1 -2
1) "mango"
2) "banana"
3) "banana"

127.0.0.1:6379> rpushx fruitsss mango
(integer) 0

127.0.0.1:6379> rpushx fruit orange
(integer) 6

127.0.0.1:6379> lpushx fruit peach
(integer) 7

127.0.0.1:6379> rpop fruit
"orange"

127.0.0.1:6379> lpop fruit
"peach"

127.0.0.1:6379> ltrim fruit 1 -2
OK

127.0.0.1:6379> lrange fruit 0 -1
1) "mango"
2) "banana"
3) "banana"

127.0.0.1:6379> ltrim fruit 1 -2
OK

127.0.0.1:6379> lrange fruit 0 -1
1) "banana"

127.0.0.1:6379> lset fruit 0 grapes
OK

127.0.0.1:6379> lrange fruit 0 -1
1) "grapes"

127.0.0.1:6379> lindex fruit 0
"grapes"

127.0.0.1:6379> lpush fruit apple orange watermelon
(integer) 4

127.0.0.1:6379> linsert fruit AFTER orange chiku
(integer) 5

127.0.0.1:6379> lrange fruit 0 -1
1) "watermelon"
2) "orange"
3) "chiku"
4) "apple"
5) "grapes"

127.0.0.1:6379> linsert fruit AFTER chiku mango
(integer) 6

127.0.0.1:6379> llen fruit
(integer) 6

127.0.0.1:6379> lrem fruit 1 mango
(integer) 1

127.0.0.1:6379> lrange fruit 0 -1
1) "watermelon"
2) "orange"
3) "chiku"
4) "apple"
5) "grapes"

127.0.0.1:6379> lrem fruit 1 apple
(integer) 1

127.0.0.1:6379> lrange fruit 0 -1
1) "watermelon"
2) "orange"
3) "chiku"
4) "grapes"

127.0.0.1:6379> lpush fruit mango mango mango
(integer) 7

127.0.0.1:6379> lrange fruit 0 -1
1) "mango"
2) "mango"
3) "mango"
4) "watermelon"
5) "orange"
6) "chiku"
7) "grapes"

127.0.0.1:6379> lrem fruit 2 mango
(integer) 2

127.0.0.1:6379> lrange fruit 0 -1
1) "mango"
2) "watermelon"
3) "orange"
4) "chiku"
5) "grapes"

127.0.0.1:6379> lpush fruit mango mango mango mango
(integer) 9

127.0.0.1:6379> lrange fruit 0 -1
1) "mango"
2) "mango"
3) "mango"
4) "mango"
5) "mango"
6) "watermelon"
7) "orange"
8) "chiku"
9) "grapes"

127.0.0.1:6379> lrem fruit 4 -4
(integer) 0


127.0.0.1:6379> lrem fruit -4 mango
(integer) 4

127.0.0.1:6379> lrem fruit -4 chiku
(integer) 1

127.0.0.1:6379> llen fruit 
(integer) 4

127.0.0.1:6379> lpush fruit mango mango mango
(integer) 7

127.0.0.1:6379> lrem fruit 0 mango
(integer) 4
