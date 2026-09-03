<!-- source: https://www.opswat.com/docs/mdcloud/operation/scan-result-page -->

# Scan Result Page

The scan results page is where you can find the results of the most recent scan you have performed. The information is grouped into several tabs, each containing specific information. Not all the tabs will be visible all the time.* E.g.: the "Extracted files" tab will only be displayed for archives, the "Sanitization" tab will only be displayed for sanitized files, and the "Proactive DLP" tab only if sensitive data was found on your file, otherwise, the tabs will be grayed out.

### [Overview](/docs/mdcloud/operation/scan-result-page#overview)

The overview section contains a summary of the scanned file:

- the file name and corresponding SHA256
- the possibility to download the sanitized version of the scanned file (if the file can be sanitized)

### [Analysis Details: Threats Prevented](/docs/mdcloud/operation/scan-result-page#analysis-details-threats-prevented)

We leverage both signature and heuristic scanning with 20+ scan engines, depending on the license tier, in the cloud to increase malware detection rates. The multiscanning result is shown in the form of a table with the following information:

You will be able to see the verdict provided by each Antivirus engine, definition update date for each Antivirus engine, and a summery with the number of antivirus engines which detected a threat.

### [Analysis Details: Proactive Data Loss Prevention (DLP)](/docs/mdcloud/operation/scan-result-page#analysis-details-proactive-data-loss-prevention-dlp)

Proactive DLP Page is designed to identify and thwart sensitive data within files, ranging from credit card numbers (CCN) and social security numbers (SSN) to IPv4 and Classless Inter-Domain Routing (CIDR).

1. To activate this feature, the initial step is to visit metadefender.opswat.com. Once there, by clicking Analyze on the left hand panel, you can easily choose and activate the Proactive DLP feature as depicted below.

2. Next step is uploading your file and allowing Proactive DLP to perform its function.
3. Once the processing is completed, the Overview page will display two new banners indicating the discovery of sensitive information in the uploaded file as below.
4. Under Static Analysis page, you will find Proactive DLP subpage with all the information about the DLP results.

You will be able to see information based on the category discovered by DLP such as the Type, Severity, Location and if the content was Redacted or not.

5. You have the option to download the sanitized version, where all sensitive information rated as Medium Certainty and above has been redacted.

### [Analysis Details: Deep CDR](/docs/mdcloud/operation/scan-result-page#analysis-details-deep-cdr)

Deep CDR stands for Deep Content Disarm and Reconstruction. What our industry leading technology does is break down a file into its most basic components, remove any potentially malicious content such as macros, and reconstruct the file without the potentially malicious content. For more information on this technology check out this page on [Deep CDR](https://www.opswat.com/technologies/data-sanitization).

On MetaDefender Cloud, scans and Deep CDR requests are performed asynchronously, and each scan request is tracked by a data ID. On this tab we display the multiscanning report of the sanitized file in order to demonstrate the effectiveness of the sanitization services as well as a link to download the sanitized file.

For the file types that don't support sanitization, this tab will be grayed out.

Please refer to [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Data Sanitization Cdr) for more information on how to leverage Deep CDR via our API.

### [The Cause of Missing Data on Given Tabs](/docs/mdcloud/operation/scan-result-page#the-cause-of-missing-data-on-given-tabs)

*If there's data missing on any of the available tabs, that means there is no information available. If you think that some information may be added, please [contact us](https://www.opswat.com/contact).
