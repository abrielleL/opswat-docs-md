<!-- source: https://www.opswat.com/docs/mdcloud/operation/homepage -->

# Homepage - MetaDefender Cloud Dashboard

## [Dashboard Page](/docs/mdcloud/operation/homepage#dashboard-page)

## [Advanced Scan Options in Analyze page](/docs/mdcloud/operation/homepage#advanced-scan-options-in-analyze-page)

The advanced scanning options can be changed by clicking Custom Scan within File Analysis, next to the Drag & drop or click to browse.

They apply when uploading a file. They are persistent, each time a user enables or disables an option, that option will be persisted for future scans.

- **Unarchiving**: when enabled and the user uploads an archive, the file will be unarchived. If not, the archive will be scanned as a single file without analyzing the files inside.
- **Archive Password:** when enabling the Unarchiving, user can upload a password protected archive and input the password for it.
- **Multiscanning**: always enabled. Perform [multiscanning](https://www.opswat.com/technologies/multiscanning) on the uploaded file.
- **Hash lookup**: enabled by default. If the option is enabled, before uploading the file, a check is performed to see if the file was previously analyzed. If results are found, the website opens at the latest analysis of the file.
- **Proactive DLP**: [Proactive Data Loss Prevention](https://www.opswat.com/technologies/proactive-data-loss-prevention) is an OPSWAT technology for preventing data leaks in files.
- **Deep CDR:** performs data sanitization on the uploaded file, if the file format is supported by our [Deep CDR technology](https://www.opswat.com/technologies/data-sanitization).
- **Sandbox:** run dynamic analysis on the files with our sandbox environment:

  - Windows 10
  - File size can go up to 2GB for Sandbox depending on the license tier
- **Private scan:** available only for paid users, with this option enabled all files scanned in private mode are not stored or shared, although scan results will remain available in the MetaDefender Cloud database.

## [Web Analysis](/docs/mdcloud/operation/homepage#web-analysis)

### [The multi-purpose search bar can be used to search for any of the key terms on our website:](/docs/mdcloud/operation/homepage#the-multi-purpose-search-bar-can-be-used-to-search-for-any-of-the-key-terms-on-our-website)

- hashes (using md5, sha1 or sha256)
- IP addresses
- URLs
- Domain addresses

When scanning a file, the service will analyze the file name and decide what operations to execute, and will always perform a hash lookup first to see if the file was already uploaded before. These options can be changed when uploading a file from the search bar with the advanced scan options.
