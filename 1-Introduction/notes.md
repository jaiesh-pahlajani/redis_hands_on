- Redis 
•   NoSQL – Key Value Store (Every data is associated with key)
•	Open Source
•	Used as cache, message broker
•	In memory(uses disk only for persistence, not for accessing data)
•	Serves Data Faster
•	Supports Data Structures such as – strings, hashes, lists, sets, sorted sets with range queries, bitmaps and hyperloglogs
•	Written in ANSI C
•	Integrate with many languages. 

- To start redis server: redis-server
- To start redis client: redis-cli

- To check if client is up: ping

- Shutdown
1. shutdown save: all keys will be available later after started
2. shutdown nosave: keys wont be saved

- If one client runs the shutdown command, the server is shut for all the clients.







