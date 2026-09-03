<!-- source: https://www.opswat.com/docs/mdcluster/operating/workflow-configuration-template -->

# Workflow Configuration Template

The Workflow templates page is found under `Workflow Management` > `Templates` after successful login.

These workflow templates define the processing methods that can be used by the rules.

MetaDefender Core comes with predefined workflow templates that can not be modified, however they can be copied and the created workflow templates are fully customizable.

Info

It is highly recommended to use less workflow template and rather more rules based on the workflow templates.

## [Workflow templates](/docs/mdcluster/operating/workflow-configuration-template#workflow-templates)

When clicking on a workflow template a windows pops up showing different tabs related to the workflow templates different kind of properties.

### [File Type](/docs/mdcluster/operating/workflow-configuration-template#file-type)

For all information about features powered by File Type, please learn more at [File Type Verification Engine](https://www.opswat.com/docs/mdcore/utilities-engines/file-type-engine).

**Detect file type mismatch** can be enabled to identify files where the file extension differs from the actual file type.

Other configurations of File Type engine can be found at [File type configurations](https://www.opswat.com/docs/mdcore/utilities-engines/filetype-configuration).

### [Archive](/docs/mdcluster/operating/workflow-configuration-template#archive)

On the Archive tab the archive handling can be enabled or disabled as well as other parameters can be set.

The max recursion level defines how deep extraction should go into the archive, the number of maximum extracted files also can be set as well as the overall maximum size of these files.

It is also possible to disable scanning the archive itself, and a timeout for the whole process can be set as well.

### [Blocklist](/docs/mdcluster/operating/workflow-configuration-template#blocklist)

Info

Since MetaDefender Core 4.19.0, user is allowed to configure to exclude child extracted files from archive file type for being blocklisted.

During scan, it is possible to create blocklists where files depending on their file type, checksum (hash), filename, extension, file size or MIME-TYPE. All of these can be stored in the fields on the Blocklist tab. Administrators can select tactic "Block All" or "Block All Except". Also it is available to blocklist all the files coming from the same group, such as Executable Files, Media Files and others.

When filtering by mime-type or filename, the filter is handled as a regular expression.

Exceptions can be defined in **Exceptions (by mime-type)** section using regular exceptions. For instance, if all office files have to be blocked except docx files, then **Office documents** group should be chosen and `^application/vnd.openxmlformats-officedocument.wordprocessingml.document$` expression should be given as exception.

More details: [Blocklist by filetype configuration](https://www.opswat.com/docs/mdcore/configuration/blocklist-by-filetype-configuration)

### [Allowlist](/docs/mdcluster/operating/workflow-configuration-template#allowlist)

During scan, it is possible to create allowlists where files depending on their file type, checksum (hash), filename, extension, file size or MIME-TYPE. All of these can be stored in the fields on the Allowlist tab. Also it is available to allowlist all the files coming from the same group, such as Text Files, Office Documents and others.

When filtering by mime-type or filename, the filter is handled as a regular expression.

Exceptions can be defined in **Exceptions (by mime-type)** section using regular exceptions. For instance, if all office files have to be allowed except docx files, then **Office documents** group should be chosen and `^application/vnd.openxmlformats-officedocument.wordprocessingml.document$` expression should be given as exception.

### [Metascan](/docs/mdcluster/operating/workflow-configuration-template#metascan)

**SKIP ANY FURTHER PROCESSINGS WITH AV SCANNING RESULT[S]:** When enabled, this setting will halt further file processing if the aggregated antivirus (AV) scan result matches any value in the selected list. This can help optimize performance by avoiding redundant processing steps when a conclusive AV result has been obtained.

**SUSPICIOUS DETECTED HANDLED AS:** By enabled, you are able to decide if Suspicious result on any particular engine is considered as Infected or No Threat Found result, and it will take consideration into overall process result which also is constraint by threat detected threshold setting.

**SCAN FAILURE THRESHOLD**: It is possible to enable and set a threshold value for failed engine results. If the number of failed results for the currently scanned object reaches this threshold, the overall result will be marked as failed. This threshold value will not influence the scan result if there are other outcomes, such as "suspicious", except in cases where the result is categorized as "infected".

**THREAT DETECTED THRESHOLD**: When checked, this setting supports two configuration options INFECTED LIMIT and the SUSPICIOUS LIMIT when SUSPICIOUS DETECTED HANDLED AS is disabled, and its handling logic will be described as following:

- If the number of infected engine results is between these values the overall result will be suspicious.
- If the INFECTED LIMIT is reached the overall result will be always infected.
- If none of them is reached the overall result will be the highest priority engine result (infected results are ignored).

Nevertheless, if **SUSPICIOUS DETECTED HANDLED AS** is also enabled, regardless of handling as Infected or No Threat Found, SUSPICIOUS LIMIT setting are no longer taken into account. The following is the handling logic:

- If the INFECTED LIMIT is reached, the overall result will be always infected.
- Otherwise, the overall result will be the highest priority engine result (infected results are ignored).

**PER ENGINE TIMEOUT / GLOBAL SCAN TIMEOUT**: The timeout for the different engines and the whole scanning process also can be set. The maximum allowed size of scanned objects can be set also on this tab as well.

### [Cloud Hash Lookup](/docs/mdcluster/operating/workflow-configuration-template#cloud-hash-lookup)

When MetaDefender Cloud workflow element is enabled, online database of MetaDefender Cloud will be used as source for hash lookups.

**Available options:**

1. **Use results**: INFECTED or ALL RESULTS If INFECTED is chosen, then only that result will be accepted as result, otherwise all type of results will be taken into account.
2. **MetaDefender Cloud API key**: An API key is necessary to have access to the MetaDefender Cloud database. API Key Information can be found on [https://metadefender.opswat.com](https://metadefender.opswat.com/), under **Account Information** page.
3. **Maximum age of scan results**: Only results that are not older than what is set here will be considered as a valid result.
4. **Excluded engines' name**: Name of the engines whose results are not to be taken into account.
5. **Minimum hit count**: To consider a verdict as a valid one, there should be at least as many result for a hash as it has been set here. (If **Use result** is set to INFECTED, then only infected results will be counted in.)
6. **Time out**: The time interval within which the response should be received from MetaDefender Cloud.

### [Deep CDR](/docs/mdcluster/operating/workflow-configuration-template#deep-cdr)

By enabling Deep CDR, one can convert from a set of supported file types into another (or the same). By doing so lot of vulnerabilities can be got rid out of rendering the resulting file be more safe. Both the types to be sanitized and the target file type can be set. To set the file types that you want to sanitize you should tick on corresponding checkboxes. In addition, you can also tick on "**ENABLE FOR ALL FILE TYPES**" to choose all supported file types. File name from sanitized files can be defined by using "OUTPUT FILENAME FORMAT" field. For usage and meanings of variables, please refer to [Setup output file name](https://www.opswat.com/docs/mdcore/deep-cdr/setup-output-file-name) page.

By default, MetaDefender Core allows files, where sanitization fails. This behavior can be overridden enabling "BLOCK FILES IF **SANITIZATION FAILS OR TIMES OUT**".

The maximum allowed time for data sanitization to be made can be configured through the "**DEEP CDR** **TIMEOUT**" and "**TRY COUNT**" options, where first one means that data sanitization should finish within the configured time frame, otherwise abort the conversion and latter means the number of times product should retry in case of a failed conversion.

When "**DISTINGUISH PARTIAL ARCHIVE SANITIZATION RESULT**" checked, MetaDefender Core will return "Partial Sanitization" processing result for Deep CDR when only some of child files in original archive files are sanitized successfully.

Beware, however, that possible data loss or change may occur during conversion, thus this feature is disabled by default.

Result of sanitization can be either downloaded on the scan page or retrieved the data ID via REST. See [Fetch processing result](https://www.opswat.com/docs/mdcluster/v2.6.0/api-gateway). Note that /hash API does not provide such information.

Length of time the system stores sanitized files can be set in **Settings > Data retention**.

### [Proactive DLP](/docs/mdcluster/operating/workflow-configuration-template#proactive-dlp)

For all information about features powered by Proactive DLP, please learn more at [Proactive DLP overview](https://www.opswat.com/docs/mdcore/proactive-dlp/user-guide).

### [Adaptive Sandbox](/docs/mdcluster/operating/workflow-configuration-template#adaptive-sandbox)

For all information about features powered by Adaptive Sandbox, please learn more at [Adaptive Sandbox overview](https://www.opswat.com/docs/mdcore/sandbox/overview).

With File type Filtering configuration, you can configure Adaptive Sandbox engine to run only for the selected file types. All the supported file types are selected by default.

With the Result Filtering configuration, you can configure Adaptive Sandbox engine to process files based on

- All Reputation results, including Known Bad or Known Good.
- All Metascan AV scan results, including No Threat Found or any threats found. By default, No Threat Found is not selected.
- All Deep CDR results, regardless of successful sanitization or failures. By default, only sanitization failures are selected.

### [SBOM](/docs/mdcluster/operating/workflow-configuration-template#sbom)

For all information about features powered by SBOM, please learn more at [Software Bill of Materials (SBOM)](https://www.opswat.com/docs/mdcore/software-bill-of-materials/overview).

### [Vulnerability](/docs/mdcluster/operating/workflow-configuration-template#vulnerability)

File-based Vulnerability Assessment scans and analyzes binaries and installers to detect known application vulnerabilities. Administrators has an ability to configure severity threshold and timeout settings.

### [Reputation](/docs/mdcluster/operating/workflow-configuration-template#reputation)

For all information about features powered by Adaptive Sandbox, please learn more at Reputation overview.

### [Country of Origin](/docs/mdcluster/operating/workflow-configuration-template#country-of-origin)

For all information about features powered by Country of Origin, please learn more at [Country of Origin](https://www.opswat.com/docs/mdcore/v5.19.0/country-of-origin/country-of-origin)

### [General](/docs/mdcluster/operating/workflow-configuration-template#general)

By enabling '**Fallback filetype detection to current extension if needed**' (enabled by default), file type detection can use the extension of the currently processed file as a helping hand. For example this could be useful, when analyzing CSV files.

Setting '**Enable file hash for only selected types**' provides a list of supported hash types.

- By default, MD5, SHA1 and SHA256 are selected. SHA512 is unselected to avoid affecting processing performance, despite not much considerable.
- SHA256 cannot be deselected.
- File-based Vulnerability Assessment engine requires SHA1. Therefore, when SHA1 is deselected, it is expected to receive the result "Skipped the assessment" from the engine.

By enabling '**Global Timeout**' (disabled by default), application provides a global timeout for entire processing applied to every scan request.

- This is only applicable to Asynchronous mode.
- When a scan request is timed out by this global processing timeout setting, the scan request will be blocked with "Global timeout exceeded" as blocked reason.
- **Note:** *This global processing timeout, when enabled, it should be greater or equal to the sum of all other engine related timeout settings such as Metascan timeout, Deep CDR timeout etc.*

By enabling '**OVERRIDE SCAN RESULTS CLASSIFIED AS ALLOWED**' it is possible to overwrite the default behavior of MetaDefender and determine which scan verdicts should result as allowed.

Scan results checked are marked as allowed.

By default only following verdicts result in allowed status:

- No Threat Detected
- Skipped Clean
- Potentially Vulnerable File
- Yara Rule Matched

By enabling '**Define time availability for workflow**', it is possible for clients to define time frames in which a specific workflow is ready to use. MetaDefender Core only accepts requests of the workflow rule if they are within available time frames defined by the rule and responds HTTP code 403 otherwise.

By selecting one of values of '**Workflow priority**', it is possible for clients to prioritize a task coming to engine.

- If there are several tasks of the same priority waiting for an engine to process, the first comes, the first is processed by the engine.
- If tasks of different priorities are waiting for an engine to process, every two tasks of high priority processed by the engine will give a chance to one single task of next lower priority to be processed.

By default, priority of all tasks coming to an engine is Medium.
