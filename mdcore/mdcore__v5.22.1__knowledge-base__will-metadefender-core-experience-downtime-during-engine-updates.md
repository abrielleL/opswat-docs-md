<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/will-metadefender-core-experience-downtime-during-engine-updates -->

# Will MetaDefender Core Experience Downtime During Engine Updates?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows and Linux systems.

MetaDefender Core is built to ensure high availability and minimize system downtime, even during antivirus engine updates.

**What Happens During an Engine Update?** MetaDefender Core includes a built-in engine failover mechanism. When multiple scanning engines are in use, this ensures uninterrupted scanning: if one engine is temporarily disabled for an update, the system continues scanning using the remaining active engines. Once the update completes, the updated engine is automatically re-enabled.

**Does the System Shut Down?** No, MetaDefender Core does **not** shut down during engine updates. Scanning and file analysis continue without interruption, maintaining protection and system stability.

### [Key Takeaways:](/docs/mdcore/v5.22.1/knowledge-base/will-metadefender-core-experience-downtime-during-engine-updates#key-takeaways)

- MetaDefender Core uses engine failover to ensure continuous operation when multiple engines are enabled.
- **Ongoing scans will continue using the current engine version and definitions without interruption. Any updated engine or database will be applied to new scan submissions as they become available.**
- **The update delay can be configured under Settings > **Module Update**. Locking the engine and database versions is available to accommodate your specific requirements.**

- It's recommended to update during low business hours to minimize interruption to daily operation.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
