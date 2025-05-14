Requirements

1. In-memory key-value storage
Use a Map in Node.js to store data in memory. Check if a key exists before returning a value.

2. Set and get operations
Use the built-in .set() and .get() methods from Map, but wrap them to add custom logic like TTL handling, memory tracking, and stats.

3. TTL (Time To Live) per key
When setting a key, store a ttl value that defines how long the key is valid. Internally, save the expiration time using Date.now() + ttl.

4. Automatic key expiration
Run a process that periodically checks all keys. If a key's TTL has expired, remove it from the cache.

5. Maximum memory limit
Allow the user to define a memory limit. Estimate the size of each entry using Buffer.byteLength(JSON.stringify(value)).
If the limit is reached, provide options:

    Remove old entries based on an eviction policy

    Or prevent new entries from being added

6. Eviction policy (FIFO or LRU)
Use a strategy to remove items when memory is full:

    LRU: Remove the least recently used key by moving accessed keys to the end of the Map (delete and re-insert them)

7. Cache hit and miss tracking
Track how many times a key is found (hit) or not found (miss). Provide simple stats to show how effective the cache is.

8. Support cache bypass (e.g., max-age=0)
If a request has a Cache-Control: max-age=0 header (or a flag like skipCache: true), skip the cache and let the backend handle the request.