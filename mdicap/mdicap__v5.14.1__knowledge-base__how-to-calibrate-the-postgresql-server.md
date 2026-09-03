<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/knowledge-base/how-to-calibrate-the-postgresql-server -->

# How to turning the performance of PostgreSQL server

The requirement to have high PostgreSQL performance: high RAM and the storage with high speed

To optimize the performance of PostgreSQL, the configuration file (postgresql.conf) can be modified with below setting:

Location of postgresql.conf (refer to: [Open Connection On PostgreSQL Server](/docs/mdicap/v5.14.1/troubleshooting/open-connection-on-postgresql-server))

Memory Settings:

- shared_buffers: amount of memory dedicated to caching data. Set to 25-40% of available RAM.
- work_mem: Allocate enough memory for sorting and hashing operations. A starting point can be 4-16 MB
- maintenance_work_mem: Use a larger value (e.g., 64-512 MB) for maintenance operations like vacuuming and index creation
- effective_cache_size: Set to 50-75% of total system memory
- autovacuum_vacuum_threshold: Use a large value (e.g. 100000) for less redundant vacuum execution
- autovacuum_vacuum_scale_factor: Set to 0 to ensure that auto-vacuum can execute properly and reduce storage space usage

Other settings:

- max_connections: The maximum number connection to PostgreSQL server at same time

Helping Tool :

- Use pgTune (<https://pgtune.leopard.in.ua/>) to generate optimized configuration settings based on your server specifications
