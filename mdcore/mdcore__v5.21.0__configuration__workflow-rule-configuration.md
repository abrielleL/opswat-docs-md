<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/configuration/workflow-rule-configuration -->

# Workflow rule configuration

The Workflow rule page is found under **Workflow > Manage Workflows** after successful login.

The rules represent different processing profiles.

The following actions are available:

- new rules can be added
- existing rules can be viewed
- existing rules can be modified
- existing rules can be deleted

Rules combine workflow templates and security zones and describe which workflows are available in a specified security zone. Multiple rules can be added for the same security zone.

## [Restriction](/docs/mdcore/v5.21.0/configuration/workflow-rule-configuration#restriction)

Once clicking on a rule, a window pops up where beside the rule properties all the chosen rule's options are shown on the different tabs.

By enabling this feature, a local scan node is able to scan the files at their original place if the files' location is allowed in the list below the checkbox. For example if this list has *C:\data* in it, then all files under that folder (e.g.: *C:\data\not_scanned\JPG_213134.jpg*) are allowed to be scanned locally if it is choosen . For testing this local scan feature, please note:

- Need to use "filepath" header while submitting a file via REST, see more at [POST File Analysis](/docs/mdcore/v5.21.0/metadefender-core#fileanalysispost).
- MetaDefender Core's web scan (localhost:8008) is not an applicable tool to test because it does not allow you to customize the scan request's header.

- **Full details**: all information for a scan is displayed.
- **Per engine result**: Scan details are displayed except per engine scan time and definition date.
- **Overall result only**: Only the overall verdict is displayed.

Processing result report will be generated dynamically based on the defined Role and Visibility settings.

There are also two special roles - **Every authenticated** refers to any logged in user, while **Everybody** refers to any user. Without belonging to any role specified within the rule, the user has no access to view the scan results. The usage of the rule to given roles can also be restricted with the **RESTRICT ACCESS TO FOLLOWING ROLES** field.

Clicking on a tab it is possible to overwrite a property that was previously defined inside the workflow template.

An option if changed will only overwrite the specific property for the underlying rule and makes no modification on the original workflow template that was choosen by the rule.

This means that several rules can be created using the same workflow template overwriting different options while the untouched properties will remain as they were set in the workflow template.

Rules are processed in order, the first matching rule will be used for the request. You can change order of rules via drag&drop in the Web Management Console. If there is no rule that matches for the client (source IP address), then the scan request will be denied.

## [Skip hash calculation](/docs/mdcore/v5.21.0/configuration/workflow-rule-configuration#skip-hash-calculation)

Info

“SKIP HASH CALCULATION” setting could be enabled under “General” tab on each desired workflow rule to make this feature triggered (disabled by default).

When enabled, expecting the following features will no longer work:

- File-based Vulnerability Assessment feature since the Vulnerability engine requires file hash value as an input.
- Reputation feature since this engine requires file hash value as an input.
- "sanitized-file-hash" header since this contains SHA256 hash value of sanitized file.
- Scan result reuse for the same hash feature since SHA256 hash value is required.

Support an option to skip hash calculation on every processing file regardless it is individual file or a part of archive.

Expecting to be used against big file processings to significantly reduce overall processing time.

In JSON scan result,

- it reveals empty values at md5, sha1, sha256, sha512.
- is_skip___hash key will be set to true should be used as a flag for client integration.

## [Local scan enablement](/docs/mdcore/v5.21.0/configuration/workflow-rule-configuration#local-scan-enablement)

By default, MetaDefender Core will always require client to upload payload data over HTTP(S) for processing, which we call it as “remote scan” with REST interface supported.

However, if the file resides on the same machine with MetaDefender Core, or resides on a local networked drive where MetaDefender Core could access and read without any authentication required, the product will support clients to specify absolute file path for processing, no need for payload uploaded in HTTP(S) body then.

Info

“ALLOW SCAN FILES ON SERVER” option could be enabled under desired workflow rule - General tab

Info

Starting with MetaDefender Core 4.19.1, the path under above setting could accept UNC path (besides local folder path)

From client side, expecting to use filepath header under HTTP(S) file request - [POST File Analysis](/docs/mdcore/v5.21.0/metadefender-core#fileanalysispost)

## [Reuse scan results for the same hash](/docs/mdcore/v5.21.0/configuration/workflow-rule-configuration#reuse-scan-results-for-the-same-hash)

The new setting under "General" section in MetaDefender Core workflow rule (disabled by default) will let authorized users configure the product to automatically reuse eligible processed results with the same hash for all other in-progress submitted requests.

MetaDefender Core customers can also specify to skip using this feature, and instead start a new processing flow as usual, on certain prior scan verdicts e.g. Failed to scan.

For now, MetaDefender Core will consider a scan request eligible for reusing the results of an earlier same-hash request when it meets all the following conditions:

- **NOT support for archive files**
- The setting "Reuse processing result" is enabled.
- The setting "Skip hash calculation" is disabled.
- The user of the earlier scan request is anonymous or the same as the current user.
- The workflow rule used for the earlier scan request must be the same as that of the current one.
- The list of verdicts that are configured on the new workflow rule must not contain the verdict of the earlier scan request.
- Request headers:

  - `metadata` header must be the same as that of the earlier scan request.
  - `engines-metadata` header must be the same as that of the earlier scan request.
- **No** engines or their databases have been updated since the earlier scan request was initiated until now.
- **No** engine status or engine configurations have been changed since the earlier scan request was initiated until now.
- **No** external scanners have been modified since the earlier scan request was initiated until now.
- **No** workflow configurations have been modified since the earlier scan request was initiated until now.
- If the earlier scan request includes a Deep CDR sanitized file, it must be present in the database as well as on disk.
- If the earlier scan request includes a Proactive DLP processed file, it must be present in both the database and on disk.
- If the "Discard processed files when the original file is blocked" feature is enabled, and processed files from Deep CDR or Proactive DLP are discarded, the conditions for reusing the scan result are **not** met.
- The lists of possible file types detected by file type engine in the earlier and current requests are the same.

Warning

Regarding to external scanner and post action, MetaDefender Core cannot detect any modification inside the scanner and/or script running the post action, so customers are advised to remove the old scanner/script and add a new one if scanner/script gets changed instead of keeping the old name for new scanner/script.

Besides that, MetaDefender Core customers have an option to let the product wait for other in-progress request (with the same hash), until it finishes and then automatically resuse to apply the final result on those waiting requests.

If the current request satisfies all conditions to reuse the processing result of an in-progress file, the current scan request will wait until:

- The file completing its processing will wake all other requests waiting for its result. If the current request reuses the processing result successfully, it will wake all others and so on.
- Reaching the wait timeout (5 minutes, cannot adjust for now), do rescan the file.

## [Discard processed files when the original file is blocked](/docs/mdcore/v5.21.0/configuration/workflow-rule-configuration#discard-processed-files-when-the-original-file-is-blocked)

This setting, located under the 'General' section in the MetaDefender Core workflow rule (disabled by default), allows you to discard processed files generated by Deep CDR or Proactive DLP if the original file is blocked.

In addition, there are two sub-options: 'Skip Deep CDR if previously blocked' and 'Skip Proactive DLP if previously blocked.' These options allow you to decide whether to **not** process the original file with Deep CDR or Proactive DLP if it was previously blocked by prior processes. These options can help improve performance by skipping Deep CDR or Proactive DLP processing in certain cases. However, if you still need the processing results from Deep CDR or Proactive DLP for specific purposes, it is recommended **not** to enable these options.

Note that these sub-options do not apply to the sanitization of archive files processed by the Archive Compression engine.

In cases where a processed file is discarded, the scan results of the original file will not be available for 'Reuse scan result', as mentioned earlier.
