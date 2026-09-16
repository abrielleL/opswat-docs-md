<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/information-regarding-how-files-are-processed-and-db-usage-by-co -->

# Information regarding how files are processed and DB usage by Core

# [**File Processing Workflow and DB Query Behavior**](/docs/mdcore/v5.22.0/knowledge-base/information-regarding-how-files-are-processed-and-db-usage-by-co#-file-processing-workflow-and-db-query-behavior)

## [**Initial Request Handling**](/docs/mdcore/v5.22.0/knowledge-base/information-regarding-how-files-are-processed-and-db-usage-by-co#-initial-request-handling)

Upon receiving a new file processing request, Metadefender Core performs the following:

- **Query Type:** `INSERT`
- **Purpose:** Log the initial state of the request in the primary request table
- **Timing:** Triggered as soon as a request enters the processing queue

This ensures traceability and readiness for downstream scanning actions.

## [**AV Engine Full Scan Integration**](/docs/mdcore/v5.22.0/knowledge-base/information-regarding-how-files-are-processed-and-db-usage-by-co#av-engine-full-scan-integration)

Once we receive the complete scan report from **Metascan AV engines**, a secondary insert operation is performed:

- **Query Type:** `INSERT` (into a different table)
- **Purpose:** Store AV scan results associated with the file
- **Timing:** Executed immediately after all AV engines finish scanning

This result set is stored separately from the initial request metadata.

## [**Final State Update**](/docs/mdcore/v5.22.0/knowledge-base/information-regarding-how-files-are-processed-and-db-usage-by-co#-final-state-update)

After all processing stages are completed—including but not limited to:

- Filetype validation engine
- AV engines
- CDR (Content Disarm & Reconstruction), if applicable
- DLP (Data Loss Prevention)

We finalize the request:

- **Query Type:** `UPDATE`
- **Purpose:** Reflect the final status of the request in the DB
- **Timing:** Triggered after successful completion of all components

## [**Summary**](/docs/mdcore/v5.22.0/knowledge-base/information-regarding-how-files-are-processed-and-db-usage-by-co#summary)

Typical file processing involves **three DB queries**:

| Stage | DB Operation | Purpose |
| --- | --- | --- |
| Request received | `INSERT` | Record initial request state |
| AV scan results completed | `INSERT` | Store detailed AV findings |
| All stages finalized | `UPDATE` | Mark the request as complete |

## [**MD Core & Reader Instances: Not Compatible**](/docs/mdcore/v5.22.0/knowledge-base/information-regarding-how-files-are-processed-and-db-usage-by-co#-md-core--reader-instances-not-compatible)

We’ve evaluated using **reader instances** in the database layer to potentially optimize performance. However:

- **Why we can't use them:** Our system requires frequent `INSERT` and `UPDATE` operations that reader instances typically do not support.
- **Implication:** MD Core must interact with write-enabled database instances to maintain data consistency and support real-time updates.
