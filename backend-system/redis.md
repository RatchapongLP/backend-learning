# Redis

- Redis (REmote DIctionary Server) is an in-memory data store server, allows for extremely fast read and write operations.
- Offers persistence options to save data to disk: RDB and AOF.
- Used as a database, cache, and message broker.
- Used for caching, session management, real-time leaderboard/analytics, and message queuing.
- Supports various data structures: strings, hashes, lists, sets, sorted sets, stream, bitmaps.
- Supports replication and clustering.

## Disk Persistence (Backup)
- **RDB (Redis Database):** Creates *point-in-time* snapshots of the *entire* dataset at specified intervals
to a single file on the server's disk (e.g., dump.rdb). Good for backups but may lose recent data in case of a crash.

- **AOF (Append Only File):** Logs every write operation command received by the server to an 
append-only file on the server's disk. When the server restarts, these commands are replayed to reconstruct the dataset in memory.
More durable than RDB but can be slower due to frequent disk writes. 

- Can be configured to use either or both methods for data persistence.