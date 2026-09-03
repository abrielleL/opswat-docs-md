<!-- source: https://www.opswat.com/docs/mdcore/operating/import-export-configuration -->

# Import/Export configuration

MetaDefender Core current configuration can be exported or a new one can be imported under the **Settings > Top Right Corner > Import or Export**

## [Export](/docs/mdcore/operating/import-export-configuration#export)

Click the export button to set the password to encrypt the archive package for exported configurations. This package will contain the following configurations:

- Workflow rules and workflow templates and security zones
- Configuration in the **Library** menu

  - Skip by Hash
  - External Scanners
  - Certificates
  - Post Actions
  - Password storage
- Almost settings on **Settings**:

  - General: queue size and Login banner
  - Email notification: all
  - Security: Password policies, Session policies, Scan from link settings
  - Network: Email server, Proxy
  - Module update: Update source, Engine dependency
  - Data Retention: Automatic deletion
  - Health Check: all
  - Central Management: all
- Users management settings: users, role, directories
- Engine status and engine advanced configuration: these options are **OFF by default,** user need to select these options if want to export:

  - Engine current status: the current status of the engines: Enable or Disable
  - Engine advanced configuration: The advanced configuration of the engines - user can find it in the Engines > Select engine, for example FileType

Yara sources setting: **OFF by default**, user need to select YARA sources in Advanced configuration when export

Why password is required?

The exported archive package must be set with a password to encrypt because it might contain sensitive data including user information.

REST API for configuration export

Details: [POST - Export configuration (new version)](/docs/mdcore/metadefender-core#adminexportv2)

## [Import](/docs/mdcore/operating/import-export-configuration#import)

Choose the exported package and also input proper password to import.

JSON config file import supported

Besides package import support, you can also import JSON config file like in MetaDefender Core v4.

JSON config file is only for MetaDefender Core workflow settings.

After the successful import, the new configurations will replace the current one.

REST API for configuration import

Details: [POST - Import configuration (new version)](/docs/mdcore/metadefender-core#adminimportv2)

**YARA sources will be not imported by default**. User need to select `Force import YARA` to import it

## [Troubleshooting](/docs/mdcore/operating/import-export-configuration#troubleshooting)

Occasionally, errors may occur during the configuration import process. This section aims to provide a clear understanding of the issue.

### [Mandatory engines are missing](/docs/mdcore/operating/import-export-configuration#mandatory-engines-are-missing)

| Name | Description |
| --- | --- |
| **Error details** |  |
| **Root-cause** | The imported zip contains the workflow rule named `File process` . In this workflow rule, under tab **General** > **Mandatory engines** had choose Proactive DLP as mandatory engine but in the current MD Core, there is no such engine, so the import failed to process. This issue also happen with all other engines: AV engines, Filetype, Archive extraction, Deep CDR, etc. Proactive DLP here is just an example. |
| **Remediation** | There are 2 options:   - Option 1: User can install the missing engine in the current MD Core, after that -> re-import the zip file. - Option 2: The user can manually modify the zip file - please refer to the section "[Manually modify the zip file](/docs/mdcore/operating/import-export-configuration#manually-modify-the-zip-file)" at the end of this page. - Open the file **wf_config_export.json** search for all the string: **process_info.mandatory_engines.engines** and remove the engine, for example: |
|  |  |

### [Excluded engines are missing](/docs/mdcore/operating/import-export-configuration#excluded-engines-are-missing)

| Name | Description |
| --- | --- |
| **Error details** |  |
| **Root-cause** | The imported zip contains the workflow rule named `File process` . In this workflow rule, under tab **Metascan** > *Excluded AV engines* had choose [Vir.IT](http://vir.it/) eXplorer as excluded engine but in the current MD Core, there is no such engine, so the import failed to process. This issue also happen with all other AV engines. |
| **Remediation** | There are 2 options:   - Option 1: User can install the missing engine in the current MD Core, after that -> re-import the zip file. - Option 2: The user can manually modify the zip file - please refer to the section "[Manually modify the zip file](/docs/mdcore/operating/import-export-configuration#manually-modify-the-zip-file)" at the end of this page. - Open the file **wf_config_export.json** search for all the string: **scan.filescan.excluded_engines** and remove the engine, for example |
|  |  |

### [The required engines in Health Check are missing](/docs/mdcore/operating/import-export-configuration#the-required-engines-in-health-check-are-missing)

| Name | Description |
| --- | --- |
| **Error details** |  |
| **Root-cause** | The imported zip has Health Check setting, in this section, it contains a setting for "Required engines" For example, in the zip file, it has configured Ahnlab as required engine for Health Check, but in the current MD Core, the license does not contains this engine, or simply this MD Core does not add license yet. |
| **Remediation** | There are 2 options:   - Option 1: User can add the license that has contains the required engines. - Option 2: The user can manually modify the zip file - please refer to the section "[Manually modify the zip file](/docs/mdcore/operating/import-export-configuration#manually-modify-the-zip-file)" at the end of this page. - Open the file **settings_export.json** search for all the string: **required_engines** and remove the engine, for example: |
|  |  |

### [The batch cert that using in the workflow is missing](/docs/mdcore/operating/import-export-configuration#the-batch-cert-that-using-in-the-workflow-is-missing)

| Name | Description |
| --- | --- |
| **Error details** |  |
| **Root-cause** | The imported zip contains the workflow rule named `File process` . In this workflow rule, under tab **General** > **Generate batch signature with certificate** had choose a search named "my cert". But in the current MD Core, there no such cert name "my cert" |
| **Remediation** | There are 2 options:   - Option 1: User can add the missing cert in Library > Certificates > Add the cert like the exported configuration. - Option 2: The user can manually modify the zip file - please refer to the section "[Manually modify the zip file](/docs/mdcore/operating/import-export-configuration#manually-modify-the-zip-file)" at the end of this page. - Open the file **wf_config_export.json** and search for all the string: allow_cert and change it to false, **allow_cert.cert** and change it to None |
|  |  |

### [The webhook signature using in the workflow is missing](/docs/mdcore/operating/import-export-configuration#the-webhook-signature-using-in-the-workflow-is-missing)

| Name | Description |
| --- | --- |
| **Error details** |  |
| **Root-cause** | The imported zip contains the workflow rule named `File process` . In this workflow rule, under tab **General** > **Webhook** had choose a signature ID: 1. But in the current MD Core, there no such signature in Library > Webhook signature |
| **Remediation** | There are 2 options:   - Option 1: User can add the missing Webhook signature in Library. - Option 2: The user can manually modify the zip file - please refer to the section "[Manually modify the zip file](/docs/mdcore/operating/import-export-configuration#manually-modify-the-zip-file)" at the end of this page. - Open the file **wf_config_export.json** search for all the string: **include_webhook_signature** and change it to **false**, "**include_webhook_signature.webhook_certificate_id ": 1** and reset this id to **0**, for example: |
|  |  |

### [Manually modify the zip file](/docs/mdcore/operating/import-export-configuration#manually-modify-the-zip-file)

We do not recommend modify the zip file manually

Please get in touch with OPSWAT for support if you have any difficulty in modifying the zip file

1. Before do anything, please back up the current file.
2. Extract the zip file, it will contain 3 files inside:

   1. wf_config_export.json → workflow rules/template related settings.
   2. settings_export.json → general configuration.
   3. skip_list.data → data from the 'skip by hash' list.
3. Open the JSON file that you want to modify
4. After the modification, save the file. **Re-zip the file again with password**. **We highly recommend using 7-Zip to compress the file**
