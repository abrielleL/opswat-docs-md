<!-- source: https://www.opswat.com/docs/mdcore/configuration/workflow-rule-configuration -->

# Workflow rule configuration

The Workflow rule page is found under **Workflow > Manage Workflows** after successful login.

The rules represent different processing profiles.

The following actions are available:

- new rules can be added
- existing rules can be viewed
- existing rules can be modified
- existing rules can be deleted

Rules combine workflow templates and security zones and describe which workflows are available in a specified security zone. Multiple rules can be added for the same security zone.

## Restriction

Once clicking on a rule, a window pops up where beside the rule properties all the chosen rule's options are shown on the different tabs.

By enabling this feature, a local scan node is able to scan the files at their original place if the files' location is allowed in the list below the checkbox. For example if this list has *C:\data* in it, then all files under that folder (e.g.: *C:\data\not_scanned\JPG_213134.jpg*) are allowed to be scanned locally if it is choosen . For testing this local scan feature, please note:

- Need to use "filepath" header while submitting a file via REST, see more at [POST File Analysis](/v5.20.0/metadefender-core/ref#fileanalysispost).
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

## Skip hash calculation

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

## Local scan enablement

By default, MetaDefender Core will always require client to upload payload data over HTTP(S) for processing, which we call it as “remote scan” with REST interface supported.

However, if the file resides on the same machine with MetaDefender Core, or resides on a local networked drive where MetaDefender Core could access and read without any authentication required, the product will support clients to specify absolute file path for processing, no need for payload uploaded in HTTP(S) body then.

Info

“ALLOW SCAN FILES ON SERVER” option could be enabled under desired workflow rule - General tab

Info

Starting with MetaDefender Core 4.19.1, the path under above setting could accept UNC path (besides local folder path)

From client side, expecting to use filepath header under HTTP(S) file request - [POST File Analysis](/v5.20.0/metadefender-core/ref#fileanalysispost)

## Reuse scan results for the same hash

The new setting under "General" section in MetaDefender Core workflow rule (disabled by default) will let authorized users configure the product to automatically reuse eligible processed results with the same hash for all other in-progress submitted requests.

MetaDefender Core customers can also specify to skip using this feature, and instead start a new processing flow as usual, on certain prior scan verdicts e.g. Failed to scan.

For now, MetaDefender Core will consider a scan request eligible for reusing the results of an earlier same-hash request when it meets all the following conditions:

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

By default, reuse applies to individual files. To reuse results for archives as well, enable **Reuse Processing Result for Archives**. This can significantly speed up repeated submissions of the same archive.

- When **Reuse Processing Result for Archives** is enabled, you can separately choose which prior verdicts should never be reused for archives.
- Reuse also works **inside** other archives: if an archive you submit contains a nested archive that was already processed, the nested archive's result is reused while the rest of the outer archive is processed normally.
- Aside from the exceptional verdicts and all the conditions above, the table below shows when an archive is re-scanned:

  | Re-scanned Condition | Why the archive is re-scanned |
  | --- | --- |
  | The archive, or any file inside it, is **password-protected / encrypted**. | Currently a stored result can't re-validate the password supplied with the new request, so the archive must be extracted and scanned again. |
  | A stored archive result that exceeded the **expansion-factor** limit is encountered **nested inside another archive**. | The expansion-factor allowance is based on the top-level file's size, so the result may differ at a different position. |
  | The archive **extraction timed out** on the earlier scan. | An extraction timeout depends on system load at the time and may not happen again, so the result is treated as non-repeatable and the archive is re-scanned. |
  | A **skip-by-hash (allow/block list) entry** that affected a file inside the archive has **changed or expired.** | The stored decision for that file is now out of date, so the archive is re-scanned to apply the current allow/block list. |

Warning

Regarding to external scanner and post action, MetaDefender Core cannot detect any modification inside the scanner and/or script running the post action, so customers are advised to remove the old scanner/script and add a new one if scanner/script gets changed instead of keeping the old name for new scanner/script.

FileType, OPSWAT Alin AI Deflection, Country of Origin and File Structure Validation always run on the newly submitted file, because they are evaluated before MetaDefender Core decides whether an earlier result can be reused. Every other engine result is taken from that earlier request.

Besides that, MetaDefender Core customers have an option to let the product wait for other in-progress request (with the same hash), until it finishes and then automatically resuse to apply the final result on those waiting requests. **This behavior does not apply to archive files.**

If the current request satisfies all conditions to reuse the processing result of an in-progress file, the current scan request will wait until:

- The file completing its processing will wake all other requests waiting for its result. If the current request reuses the processing result successfully, it will wake all others and so on.
- Reaching the wait timeout (5 minutes, cannot adjust for now), do rescan the file.

## Discard processed files when the original file is blocked

This setting, located under the 'General' section in the MetaDefender Core workflow rule (disabled by default), allows you to discard processed files generated by Deep CDR or Proactive DLP if the original file is blocked.

In addition, there are two sub-options: 'Skip Deep CDR if previously blocked' and 'Skip Proactive DLP if previously blocked.' These options allow you to decide whether to **not** process the original file with Deep CDR or Proactive DLP if it was previously blocked by prior processes. These options can help improve performance by skipping Deep CDR or Proactive DLP processing in certain cases. However, if you still need the processing results from Deep CDR or Proactive DLP for specific purposes, it is recommended **not** to enable these options.

Note that these sub-options do not apply to the sanitization of archive files processed by the Archive Compression engine.

In cases where a processed file is discarded, the scan results of the original file will not be available for 'Reuse scan result', as mentioned earlier.
