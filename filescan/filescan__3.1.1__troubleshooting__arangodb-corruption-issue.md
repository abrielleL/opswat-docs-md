<!-- source: https://www.opswat.com/docs/filescan/3.1.1/troubleshooting/arangodb-corruption-issue -->

# ArangoDB corruption issue

In some rare cases, ArangoDB might fail to restart after a compaction operation.

In this situation, `docker ps` shows that the `graphdb` (arangodb) container is restarting continuously and the `webservice` container becomes `unhealthy` because of that:

To see the underlying issue, please check the logs of the `graphdb` container and look for the fatal error: **"Corruption: Compaction sees out-of-order keys."**

$ sudo docker logs -f graphdb
2024-10-03T14:40:34.843883Z [1-2] INFO [e52b0] {general} ArangoDB 3.12.2 [linux] 64bit, using jemalloc, build refs/tags/v3.12.2 154c4c5632c, VPack 0.2.1, RocksDB 7.2.0, ICU 64.2, V8 12.1.165, OpenSSL 3.3.1 4 Jun 2024, build-id: 5c4ea43cfa23ed3f6634a7bedae08e63f7f75362
...
2024-10-03T14:40:35.001667Z [1-11] ERROR [fae2c] {rocksdb} RocksDB encountered a background error during a compaction operation: Corruption: Compaction sees out-of-order keys.; The database will be put in read-only mode, and subsequent write errors are likely. It is advised to shut down this instance, resolve the error offline and then restart it.
2024-10-03T14:40:35.035726Z [1-2] FATAL [d61a8] {engines} Error storing value for --database.extended-names in storage engine: Corruption: Compaction sees out-of-order keys.

This is a known issue in ArangoDB: <https://github.com/arangodb/arangodb/issues/20841>

Until ArangoDB releases an automated solution to recover from this corrupted state, the simplest solution is purging the Arango database files from the `/data/graphdb/fsio` folder (after stopping the sandbox service):

Warning

Purging the database files will impact the Advanced Search (Hunting) functionality: All previous scan reports will remain available in the system, but older scans will be excluded from advanced search operations.

BashCopysudo service sandbox stop
sudo rm -rf /data/graphdb/fsio/*
sudo service sandbox start

After this purge, ArangoDB will start from a clean slate and the Sandbox `webservice` can function properly.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
