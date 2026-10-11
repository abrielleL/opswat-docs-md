<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/what-is-the-recommended-skip-hash-list-size-in-metadefender-core -->

# What Is the Recommended Skip Hash List Size in MetaDefender Core Without Impacting Performance?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to MetaDefender Core since version v5.12.0.

The Skip By Hash feature in MetaDefender Core allows administrators to define Allowlist, Blocklist, and Skip Engines rules using file hashes.

This article clarifies system limits, performance behavior, and recommended sizing guidance.

1. **Is There a Maximum Number of Hashes?**

There is no defined hard limit on the total number of hashes that can be stored in the Skip Hash list. However, the CSV import size is limited to a maximum of 500 MB per file.

Performance testing shows:

- Importing **1 million hashes** took approximately **115 seconds**
- Test environment:

  - MetaDefender Core 5.17.1 standalone
  - Windows VM
  - 8 CPUs
  - 16 GB RAM

This confirms that MetaDefender Core can support very large skip lists.

2. **How Skip Hash Checking Works**

When a file is scanned:

- The file hash is calculated.
- MetaDefender Core checks whether the hash exists in the Skip List stored in the local database.

The hash comparison itself is lightweight and does not impact Core performance.

3. **Performance Impact by Hash Volume**

While there is no fixed maximum, practical performance behavior typically follows:

| Total Skip Hashes | Expected Performance Impact (Well-Sized DB) |
| --- | --- |
| < 500K | Negligible impact |
| ~1M | Very low impact (validated test) |
| 1M–5M | Generally safe with proper indexing |
| 5M–10M | Increased DB dependency; tuning required |
| >10M | Requires strong database sizing and monitoring |

Important: If the PostgreSQL instance is:

- Shared with other applications
- Under-provisioned
- Running on slow disk

Performance degradation may appear earlier (even at 2–3 million entries).

4. **Import Behavior and Runtime Impact**

During CSV import:

- Scan service is not interrupted
- Duplicate cleanup increases processing time (If the CSV contains hashes that already exist in the Skip Hash list, the system needs to check and update those entries. This “duplicate handling” takes extra time, so the import process may be slower depending on how many duplicates are present).

Large imports increase database write activity but do not stop scanning.

5. **Recommended Safe Practice**

For stable and predictable performance:

- Keep Skip Hash list ideally under 5 million entries
- Use a dedicated SQL instance
- Ensure proper indexing
- Use SSD/NVMe storage
- Monitor:

  - DB CPU usage
  - Disk I/O latency
  - Query execution time
- Perform large imports during maintenance windows
- Avoid parallel CSV uploads

6. **Final Recommendation**

There is no official maximum number of hashes, but performance is infrastructure-dependent.

For most production environments:

1–5 million hashes can be handled without noticeable performance impact when properly sized. Above that, performance depends heavily on database capacity and tuning.

If planning to scale beyond 5–10 million entries, performance testing in a staging environment is strongly recommended.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
