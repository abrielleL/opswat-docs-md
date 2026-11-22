<!-- source: https://www.opswat.com/docs/mdcluster/operating/operating-processing-history -->

# Processing History

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
### Processing history

The Processing History section (**History** > **Processing**) shows information on all scans made on MetaDefender Cluster (MD Cluster). Search and Filter are also supported against each scan result attribute. The user can search based on the following:

- MD5, SHA1, SHA256, or SHA512 hashes.
- File name (and you can limit search result for a specific scan result, and for specific username who submitted files).
- Source (IP address).
- User name.

### Scan result

Selecting a file in the Processing History will show the Scan Result of the file. Here the user can see the result of each engine.

### Filter

In **Display Options**, the **Filter** tab offers multiple filtering options, such as the scan status, the instance that handled the file, the action taken on the file, the workflow used for processing the file, and more. Use **Date and Time** to limit the results to the date and time of the process. Users can easily combine these to find their desired results.

### Display settings

The **Duration Format** tab in **Display Options** will allow the user to change the format of the Duration column. There are 3 options to choose from:

- Default format: Shown as milliseconds or ms.
- Time format: Shown as d h:m:s.ms.
- Short format: Shown as d h m s ms.

### Cleanup

To delete Processing History, click the **Cleanup** icon next to **Date and Time** at the top right. In the **Delete Processing History** dialog, select a time range (for example, **Older than 1 week**, or **Clean all**) and confirm.

**Callback and processing history retention**

In some cases, a callback may not be delivered if its processing history record is removed by the retention policy before MD Cluster Callback Service processes the request. Without this record, the Callback Service cannot retrieve and send the scan result or update the callback delivery status.
