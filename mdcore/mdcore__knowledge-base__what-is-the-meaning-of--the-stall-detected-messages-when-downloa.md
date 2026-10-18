<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/what-is-the-meaning-of--the-stall-detected-messages-when-downloa -->

# What is the meaning of the Stall detected messages when downloading engines on MetaDefender Core?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check your version**

This article applies to all MetaDefender V5 releases deployed on Windows or Linux system

## [**Symptoms**](/docs/mdcore/knowledge-base/what-is-the-meaning-of--the-stall-detected-messages-when-downloa#symptoms)

Engine or database updates fail to complete, and the MetaDefender Core log records repeated "Stall detected" entries for a download, followed by the download being cancelled and the partial package removed. The entries look similar to this:

[INFO ] (common.communication) Stall detected for download, url='.../eset_1_windows-database-1691385165.zip' [msgid: 601]
[INFO ] (common.communication) Stall detected for download, url='.../eset_1_windows-database-1691385165.zip' [msgid: 601]
[WARNING] (common.communication) Download failed because of stall, url='.../eset_1_windows-database-1691385165.zip' [msgid: 602]
[WARNING] (common.communication) Error while downloading file, error='OperationCanceledError', errorDetails='Operation canceled' [msgid: 485]
[ERROR ] (common.update) Download error occurred, removing downloaded package [msgid: 838]
[INFO ] (common.update) Package has been marked failed [msgid: 1097]
[INFO ] (common.update) Package folder was removed [msgid: 1786]

The key indicators are the repeated `Stall detected for download [msgid: 601]` messages and the subsequent `Download failed because of stall [msgid: 602]`.

## [**Root cause**](/docs/mdcore/knowledge-base/what-is-the-meaning-of--the-stall-detected-messages-when-downloa#root-cause)

A "stall" means MetaDefender Core opened the connection to the OPSWAT update server but stopped receiving data for long enough that the transfer was considered inactive. After several stall detections, MetaDefender Core cancels the download, discards the incomplete package, and marks the update as failed.

This is a network condition, not a fault in MetaDefender Core.

The connection to `update.dl.opswat.com` is being obstructed or interrupted so that data cannot flow through reliably. Common causes include:

- A proxy, firewall, or SSL/TLS inspection device that buffers, throttles, or interrupts the connection
- An intrusion prevention system (IPS) or deep packet inspection rule that slows or resets the session
- Bandwidth shaping or rate limiting on the path to the internet
- General packet loss, latency, or an unstable route to the OPSWAT content delivery network

## [**Resolution**](/docs/mdcore/knowledge-base/what-is-the-meaning-of--the-stall-detected-messages-when-downloa#resolution)

Verify and stabilize network connectivity between MetaDefender Core and the OPSWAT update server.

1. Confirm the server can reach the OPSWAT update endpoint over HTTPS (port 443):

   - `update.dl.opswat.com`
2. If a proxy is used, confirm it is configured correctly in MetaDefender Core and that it is not buffering or timing out large transfers.
3. Ask your network team to check whether any firewall, proxy, SSL/TLS inspection, IPS, or content-filtering device is inspecting, throttling, or resetting traffic to `update.dl.opswat.com`. Where possible, exclude the OPSWAT update domains from inspection and throttling.
4. Review bandwidth or rate-limiting policies that could interrupt sustained downloads, especially for the larger engine packages.
5. Retry the engine update after the network path has been verified.

**Support:**

If you need further assistance, please contact OPSWAT Support through the [OPSWAT Portal](https://my.opswat.com/) or your assigned support representative.
