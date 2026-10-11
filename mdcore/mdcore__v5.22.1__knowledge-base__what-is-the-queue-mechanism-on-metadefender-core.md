<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/what-is-the-queue-mechanism-on-metadefender-core -->

# What is the Queue Mechanism on Metadefender Core?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

### [MetaDefender Core is equipped with a robust queue mechanism designed to efficiently manage high-volume data processing tasks, such as file scanning. This article outlines the core concepts of the queue mechanism, its behavior, and configuration parameters.](/docs/mdcore/v5.22.1/knowledge-base/what-is-the-queue-mechanism-on-metadefender-core#metadefender-core-is-equipped-with-a-robust-queue-mechanism-designed-to-efficiently-manage-high-volume-data-processing-tasks-such-as-file-scanning-this-article-outlines-the-core-concepts-of-the-queue-mechanism-its-behavior-and-configuration-parameters)

## [Overview of the Queue Mechanism](/docs/mdcore/v5.22.1/knowledge-base/what-is-the-queue-mechanism-on-metadefender-core#overview-of-the-queue-mechanism)

MetaDefender Core organizes its file processing tasks using a queue system. This allows the platform to handle incoming data in a controlled and orderly manner.

- **Processing Threads (Workflows):** Each item in the queue is processed by a separate workflow, or thread, on the system.
- **Processing Order:** By default, items are handled on a **first come, first served** basis. While this ensures fairness, it does **not** guarantee a predictable processing time for each item or the overall queue. To help align file processing with business priorities, MetaDefender Core allows you to set processing priorities based on the workflow in use. This can be configured under the **"General"** tab of each workflow.
- **Archive File Handling:** By default, MetaDefender Core reserves **25% of the total queue size** specifically for archive processing. This cap applies to **all archives in the queue collectively**, not per archive. For example, submitting a single archive will only occupy up to 25% of the total queue, regardless of the archive's internal content. Starting with MetaDefender Core v5.14.1, the value is configurable up to 75% of the total queue. This setting can be adjusted from the **Settings > General** tab. This design ensures that:

  - Additional file submissions are not blocked by resource-heavy archive extraction.
  - There’s capacity for **parallel processing** across different file types.

## [Queue Size](/docs/mdcore/v5.22.1/knowledge-base/what-is-the-queue-mechanism-on-metadefender-core#queue-size)

- **Default Size:** The default queue size is **500 items**. Starting with MetaDefender Core v5.11.0, the value can be set directly in the UI via the **Settings > General** tab.
- **Monitoring Queue Status:** You can check the number of queued items in the **Dashboard** > **System Health** > **Current Processing Slots** tab by using the REST API endpoint `GET /stat/nodes`

## [Summary](/docs/mdcore/v5.22.1/knowledge-base/what-is-the-queue-mechanism-on-metadefender-core#summary)

The queue mechanism in MetaDefender Core v5 is designed to balance performance and stability under high data loads. With controlled archive handling and configurable queue size, the system ensures efficient resource allocation and throughput.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).
