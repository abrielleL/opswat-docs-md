<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/how-can-i-improve-folder-discovery-and-scanning-performance-in-m -->

# How Can I Improve Folder Discovery and Scanning Performance in MetaDefender Storage Security?

This article applies to all MetaDefender Storage Security releases deployed on Windows or Linux systems.

When using MetaDefender Storage Security (MDSS) to scan large or deeply nested folder structures, you may notice that the initial discovery process takes longer than expected. This article explains how MDSS performs folder discovery, why deep or complex directory structures can impact scanning speed, and how to optimize performance using event-based scanning.

The information provided applies to **all supported storage services** (e.g., Box, Amazon S3, Google Drive, local storage).

### [**Discovery Service Workflow**](/docs/mdss/knowledge-base/how-can-i-improve-folder-discovery-and-scanning-performance-in-m#discovery-service-workflow)

MDSS uses a **Discovery Service** to locate and prepare files for malware scanning. The workflow proceeds as follows:

1. **Initial Discovery**

   - MDSS begins by enumerating all objects (files and folders) at the root level of the designated storage path.
2. **Analysis Phase**

   - Each discovered object is analyzed:

     - **Files** are immediately sent to MetaDefender Core for malware scanning.
     - **Folders** initiate a **recursive discovery** process, scanning their contents level by level.
3. **Sequential Traversal**

   - Discovery proceeds **hierarchically**, meaning that deeper folder structures take longer to complete because each subfolder is processed sequentially.

### [**How to Improve Scanning Performance**](/docs/mdss/knowledge-base/how-can-i-improve-folder-discovery-and-scanning-performance-in-m#how-to-improve-scanning-performance)

If your environment contains a large number of folders or deep directory trees, the following methods can significantly reduce discovery and scanning time:

#### [**1. Implement Event-Based Scanning**](/docs/mdss/knowledge-base/how-can-i-improve-folder-discovery-and-scanning-performance-in-m#1-implement-event-based-scanning)

Instead of relying solely on recursive discovery scans, use **Event-Based scanning** (also known as Real-Time Protection) to process files as they are created or modified.

**Benefits:**

- Files are scanned immediately, without full-folder traversal.
- Reduces overall discovery and processing time.
- Optimizes resource utilization and system performance.

#### [**2. Limit the Scope of Initial Discovery**](/docs/mdss/knowledge-base/how-can-i-improve-folder-discovery-and-scanning-performance-in-m#2-limit-the-scope-of-initial-discovery)

If full discovery is required:

- Target only critical folders.
- Adjust scan depth (if applicable).
- Schedule discovery tasks during off-peak hours to minimize performance impact.

### [**Additional Resources**](/docs/mdss/knowledge-base/how-can-i-improve-folder-discovery-and-scanning-performance-in-m#additional-resources)

- [**Event-Based Handling Overview**](https://www.opswat.com/docs/mdss/configuration/event-based-handling)
- [**Event-Based Request Format**](https://www.opswat.com/docs/mdss/configuration/event-based-request-format)

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
