<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/how-does-the-icap-server-handle-a-batch-when-one-file-fails- -->

# How Does the ICAP Server Handle a Batch When One File Fails?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info:

- This article applies to all MD ICAP versions
#### [**Summary:**](/docs/mdicap/v5.15.0/knowledge-base/how-does-the-icap-server-handle-a-batch-when-one-file-fails-#summary)

This article explains the behavior of the ICAP Server when processing a batch of files, particularly when one of the files fails during submission to the MetaDefender Core (MD-Core) engine.

#### [Behavior Overview](/docs/mdicap/v5.15.0/knowledge-base/how-does-the-icap-server-handle-a-batch-when-one-file-fails-#behavior-overview)

When the ICAP Server receives a request that contains **multipart form**, it processes the request in the following sequence:

- **Batch Initialization**

  1. The ICAP Server initializes a new batch to group the incoming files.
  2. **Parallel Submission to MD-Core**
  3. Each part are sent to MD-Core concurrently using the API: `POST /file`

*Note: The default maximum concurrency is 5.*

- **If a File Fails During Submission from MD Core**

  - When a file fails to submit, the ICAP Server will trigger a batch scan cancellation.
  - ***Note:*** *Batch scan cancellation currently only occurs when a file POST request to MD Core fails. Other failure scenarios are under review for future enhancements and are not yet supported.*

Support:

If you require further assistance, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
