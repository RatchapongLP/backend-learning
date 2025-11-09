# Redis

- Redis (REmote DIctionary Server) is an in-memory data store server, allows for extremely fast read and write operations.

- Offers persistence options to save data to disk: RDB and AOF.

- Used as a database, cache, and message broker.

- Used for caching, session management, real-time leaderboard/analytics, and message queuing.

- Supports various data structures: strings, hashes, lists, sets, sorted sets, stream, bitmaps.

- Supports replication and clustering.

## Why is Redis Fast?
- **In-Memory Storage:** All data is stored in RAM, allowing for low-latency access.

- **Single-Threaded Architecture:** Uses an event-driven, non-blocking I/O model, avoiding context switching overhead.

- **Efficient Data Structures:** Optimized for fast operations on various data types.

- **Lightweight Protocol::** Minimal protocol overhead and server-side processing.

- **Client-Side Caching:** Some Redis clients support client-side caching, reducing the need to fetch frequently accessed data from the server.

## Disk Persistence (Backup)
- Use background threads to save data to disk without blocking main operations.

- Can be configured to use either or both methods for data persistence.

### AOF (Append Only File)
- Logs every write operation command received by the server to an append-only file on the server's disk.

- When the server restarts, these commands are replayed to reconstruct the dataset in memory.

**Advantages of AOF**
1. Better Durability: AOF can logs every write operation with `appendfsync always`, reducing the risk of data loss.

2. Human-Readable Format: AOF files store the commands in a plain text format, easy to inspect and understand.

**Disadvantages of AOF**
1. Larger File Size: AOF files can be significantly larger than RDB files, as they store every write operation.

2. Slower Recovery: The recovery/reconstruction process of AOF is slower than RDB, as Redis needs to replay all the logged commands.

### RDB (Redis Database)
- Creates *point-in-time* snapshots of the *entire* dataset at specified intervals to a single file on the server's disk (e.g., dump.rdb).

**Advantages of RDB**
1. Compact Data Format: RDB files are highly compressed and optimized, which reduces the disk space usage.

2. Faster Recovery: Since RDB files contain a full snapshot of the data, the recovery process is faster than AOF.

3. Minimal Performance Impact: The RDB snapshotting process has minimal impact on Redis performance, as it occurs in the background.

**Disadvantages of RDB**

1. Data Loss: RDB snapshots are taken periodically, which means that in case of a system crash.

2. Forking Overhead: The Redis process needs to fork a child process to create the RDB snapshot, which can be resource-intensive for large datasets.