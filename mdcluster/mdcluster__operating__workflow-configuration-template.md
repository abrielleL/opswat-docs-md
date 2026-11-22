<!-- source: https://www.opswat.com/docs/mdcluster/operating/workflow-configuration-template -->

# Workflow Configuration Template

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

The Workflow templates page is found under `Workflow`: on the **Workflows** page, click the **...** (more) button and select `Manage Templates`.

These workflow templates define the processing methods that can be used by the rules.

MetaDefender Core comes with predefined workflow templates that can not be modified, however they can be copied and the created workflow templates are fully customizable.

Info

It is highly recommended to use less workflow template and rather more rules based on the workflow templates.

## [Workflow templates](/docs/mdcluster/operating/workflow-configuration-template#workflow-templates)

When clicking on a workflow template, the **Template Configuration** page opens, listing the different kinds of workflow template properties as sections on the left side.

### [File Type](/docs/mdcluster/operating/workflow-configuration-template#file-type)

For all information about features powered by File Type, please learn more at [File Type Verification Engine](https://www.opswat.com/docs/mdcore/utilities-engines/file-type-engine).

**Detect File Type Mismatch** can be enabled to identify files where the file extension differs from the actual file type.

Other configurations of File Type engine can be found at [File type configurations](https://www.opswat.com/docs/mdcore/utilities-engines/filetype-configuration).

### [Archive](/docs/mdcluster/operating/workflow-configuration-template#archive)

In the Archive section the archive handling can be enabled or disabled (**Enable Archive Extraction**) as well as other parameters can be set.

The **Max Nesting Level** defines how deep extraction should go into the archive, the **Max Number of Files Extracted** also can be set as well as the overall maximum size of these files (**Max Total Size of Extracted Files**).

It is also possible to disable scanning the archive itself (**Enable Scan of Original Unextracted Archive**), and a timeout for the whole process can be set as well (**Archive Analysis Timeout**).

### [Blocklist](/docs/mdcluster/operating/workflow-configuration-template#blocklist)

Info

Since MetaDefender Core 4.19.0, user is allowed to configure to exclude child extracted files from archive file type for being blocklisted.

During scan, it is possible to create blocklists where files depending on their file type, checksum (hash), filename, extension, file size or MIME-TYPE. All of these can be stored in the fields in the Blocklist section. Administrators can select tactic "Block All" or "Block All Except". Also it is available to blocklist all the files coming from the same group, such as Executable Files, Media Files and others.

When filtering by mime-type or filename, the filter is handled as a regular expression.

Exceptions can be defined in **Exceptions (by Mime-type)** section using regular exceptions. For instance, if all office files have to be blocked except docx files, then **Office documents** group should be chosen and `^application/vnd.openxmlformats-officedocument.wordprocessingml.document$` expression should be given as exception.

More details: [Blocklist by filetype configuration](https://www.opswat.com/docs/mdcore/configuration/blocklist-by-filetype-configuration)

### [Allowlist](/docs/mdcluster/operating/workflow-configuration-template#allowlist)

During scan, it is possible to create allowlists where files depending on their file type, checksum (hash), filename, extension, file size or MIME-TYPE. All of these can be stored in the fields in the Allowlist section. Also it is available to allowlist all the files coming from the same group, such as Text Files, Office Documents and others.

When filtering by mime-type or filename, the filter is handled as a regular expression.

Exceptions can be defined in **Exceptions (by Mime-type)** section using regular exceptions. For instance, if all office files have to be allowed except docx files, then **Office documents** group should be chosen and `^application/vnd.openxmlformats-officedocument.wordprocessingml.document$` expression should be given as exception.

### [Metascan™](/docs/mdcluster/operating/workflow-configuration-template#metascan)

**Skip Any Further Processings with Av Scanning Result[s]:** When enabled, this setting will halt further file processing if the aggregated antivirus (AV) scan result matches any value in the selected list. This can help optimize performance by avoiding redundant processing steps when a conclusive AV result has been obtained.

**Handle Suspicious Detection As:** By enabled, you are able to decide if Suspicious result on any particular engine is considered as Infected or No Threat Found result, and it will take consideration into overall process result which also is constraint by threat detected threshold setting.

**Scan Failure Threshold**: It is possible to enable and set a threshold value for failed engine results. If the number of failed results for the currently scanned object reaches this threshold, the overall result will be marked as failed. This threshold value will not influence the scan result if there are other outcomes, such as "suspicious", except in cases where the result is categorized as "infected".

**AV Engine Thresholds**: When enabled, this setting supports two configuration options **Infected Threshold** and **Suspicious Threshold** when **Handle Suspicious Detection As** is disabled, and its handling logic will be described as following:

- If the number of infected engine results is between these values the overall result will be suspicious.
- If the **Infected Threshold** is reached the overall result will be always infected.
- If none of them is reached the overall result will be the highest priority engine result (infected results are ignored).

Nevertheless, if **Handle Suspicious Detection As** is also enabled, regardless of handling as Infected or No Threat Found, **Suspicious Threshold** setting are no longer taken into account. The following is the handling logic:

- If the **Infected Threshold** is reached, the overall result will be always infected.
- Otherwise, the overall result will be the highest priority engine result (infected results are ignored).

**Timeouts** (**Per AV Engine Scan** / **Global Scan**): The timeout for the different engines and the whole scanning process also can be set. The maximum allowed size of scanned objects is set in the **General** section (**Max Sizes** > **File Scan**).

### [Cloud Hash Lookup](/docs/mdcluster/operating/workflow-configuration-template#cloud-hash-lookup)

When MetaDefender Cloud workflow element is enabled, online database of MetaDefender Cloud will be used as source for hash lookups.

**Available options:**

1. **Use Results**: INFECTED or ALL RESULTS If INFECTED is chosen, then only that result will be accepted as result, otherwise all type of results will be taken into account.
2. **MetaDefender Cloud API Key**: An API key is necessary to have access to the MetaDefender Cloud database. API Key Information can be found on [https://metadefender.opswat.com](https://metadefender.opswat.com/), under **Account Information** page.
3. **Max Age of Processing Results**: Only results that are not older than what is set here will be considered as a valid result.
4. **Min Hit Count**: To consider a verdict as a valid one, there should be at least as many result for a hash as it has been set here. (If **Use Results** is set to INFECTED, then only infected results will be counted in.)
5. **Cloud Hash Lookup Timeout**: The time interval within which the response should be received from MetaDefender Cloud.

### [Deep CDR](/docs/mdcluster/operating/workflow-configuration-template#deep-cdr)

By enabling Deep CDR, one can convert from a set of supported file types into another (or the same). By doing so lot of vulnerabilities can be got rid out of rendering the resulting file be more safe. Both the types to be sanitized and the target file type can be set. The file types to sanitize are set under **Enable for Filetypes**: click **Edit** and choose the file types or groups in the **Add File Type** dialog (for example **All File Types**). The number of selected types is shown in **File Types Selected**. File name from sanitized files can be defined by using "**Output Filename Format**" field. For usage and meanings of variables, please refer to [Setup output file name](https://www.opswat.com/docs/mdcore/deep-cdr/setup-output-file-name) page.

By default, MetaDefender Core allows files, where sanitization fails. This behavior can be overridden enabling "**Block Files if the Process Fails or Times Out**".

The maximum allowed time for data sanitization to be made can be configured through the **Timeouts** > "**Deep CDR**" and "**Retry in Case of Failure**" (**Number of Retries**) options, where first one means that data sanitization should finish within the configured time frame, otherwise abort the conversion and latter means the number of times product should retry in case of a failed conversion.

When **Distinguish Partial Archive Process Result** is enabled (in the **Compression** section, under **Archive Sanitization**), MetaDefender Core will return "Partial Sanitization" processing result for Deep CDR when only some of child files in original archive files are sanitized successfully.

Beware, however, that possible data loss or change may occur during conversion, thus this feature is disabled by default.

Result of sanitization can be either downloaded on the scan page or retrieved the data ID via REST. See [Fetch processing result](https://www.opswat.com/docs/mdcluster/v2.6.0/api-gateway). Note that /hash API does not provide such information.

Length of time the system stores sanitized files can be set in **Settings > Data Retention**.

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

For all information about features powered by Reputation, please learn more at Reputation overview.

### [Country of Origin](/docs/mdcluster/operating/workflow-configuration-template#country-of-origin)

For all information about features powered by Country of Origin, please learn more at [Country of Origin](https://www.opswat.com/docs/mdcore/v5.19.0/country-of-origin/country-of-origin)

### [General](/docs/mdcluster/operating/workflow-configuration-template#general)

By enabling '**Enable Extension-Based Processing Fallback**' in the **File Type** section (enabled by default), file type detection can use the extension of the currently processed file as a helping hand. For example this could be useful, when analyzing CSV files.

Setting '**Enable File Hash for Only Selected Types**' provides a list of supported hash types.

- By default, MD5, SHA1 and SHA256 are selected. SHA512 is unselected to avoid affecting processing performance, despite not much considerable.
- SHA256 cannot be deselected.
- File-based Vulnerability Assessment engine requires SHA1. Therefore, when SHA1 is deselected, it is expected to receive the result "Skipped the assessment" from the engine.

The size limit for files submitted by link is set in **Max Sizes** > **URL File Download**.

By enabling '**Enable Global Timeout**' (disabled by default), application provides a global timeout for entire processing applied to every scan request.

- This is only applicable to Asynchronous mode.
- When a scan request is timed out by this global processing timeout setting, the scan request will be blocked with "Global timeout exceeded" as blocked reason.
- **Note:** *This global processing timeout, when enabled, it should be greater or equal to the sum of all other engine related timeout settings such as Metascan timeout, Deep CDR timeout etc.*

By enabling '**Processing Results to Be Classified as Allowed**' it is possible to overwrite the default behavior of MetaDefender and determine which scan verdicts should result as allowed.

Scan results checked are marked as allowed.

By default only following verdicts result in allowed status:

- No Threat Detected
- Potentially Vulnerable File
- Yara Rule Matched

By enabling '**Define Time Availability for Workflow**', it is possible for clients to define time frames in which a specific workflow is ready to use. MetaDefender Core only accepts requests of the workflow rule if they are within available time frames defined by the rule and responds HTTP code 403 otherwise.

By selecting one of values of '**Workflow Priority**', it is possible for clients to prioritize a task coming to engine.

- If there are several tasks of the same priority waiting for an engine to process, the first comes, the first is processed by the engine.
- If tasks of different priorities are waiting for an engine to process, every two tasks of high priority processed by the engine will give a chance to one single task of next lower priority to be processed.

By default, priority of all tasks coming to an engine is Medium.
