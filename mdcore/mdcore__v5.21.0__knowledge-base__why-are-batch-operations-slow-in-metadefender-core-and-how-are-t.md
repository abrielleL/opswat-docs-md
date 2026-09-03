<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/why-are-batch-operations-slow-in-metadefender-core-and-how-are-t -->

# Why are batch operations slow in MetaDefender Core and how are they resolved in version 5.14.0?

This article applies to all MD Core prior to version 5.14.0

### [**Issue:**](/docs/mdcore/v5.21.0/knowledge-base/why-are-batch-operations-slow-in-metadefender-core-and-how-are-t#issue)

Significant delays during batch operations, specifically when executing API calls such as:

- `POST /file/batch/<batch_id>/close`
- `GET /file`
- `POST /admin/batch/closeall`

PostgreSQL logs revealed that the function `scan.getFirstRcFile(BIGINT)` was executing repeatedly and taking longer time to query:

`[11076] LOG: duration: 6552.132 ms execute : SELECT * FROM scan.getFirstRcFile($1::BIGINT); 2025-10-27 00:00:17.705 IST [9804] LOG: duration: 10619.755 ms execute : SELECT * FROM scan.getFirstRcFile($1::BIGINT);`

These delays led to bottlenecks in the batch-processing workflow.

### [**Root Cause:**](/docs/mdcore/v5.21.0/knowledge-base/why-are-batch-operations-slow-in-metadefender-core-and-how-are-t#root-cause)

In earlier versions, batch-scan requests triggered the `scan.getFirstRcFile(BIGINT)` query multiple times for each file within a batch. When processing large numbers of files, this resulted in cumulative delays and degraded overall performance.

### [**Resolution:**](/docs/mdcore/v5.21.0/knowledge-base/why-are-batch-operations-slow-in-metadefender-core-and-how-are-t#resolution)

The issue has been addressed in version 5.14.0

<https://www.opswat.com/docs/mdcore/v5.14.0/release-notes>

The Close Batch workflow has been refactored so that it no longer invokes `scan.getFirstRcFile(BIGINT)`. The `GET /file` API has been optimized to reduce query overhead and avoid repeated calls to this function.

As a result, PostgreSQL logs in version 5.14.0 no longer display long-running `scan.getFirstRcFile($1::BIGINT)` queries during the impacted APIs.

Support:

If you require further assistance, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
