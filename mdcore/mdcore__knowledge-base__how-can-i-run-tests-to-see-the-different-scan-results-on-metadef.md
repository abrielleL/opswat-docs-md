<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-can-i-run-tests-to-see-the-different-scan-results-on-metadef -->

# How can I run tests to see the different scan results on MetaDefender Core?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

**The following test cases explain how to obtain the possible scan results from MetaDefender Core:**

- **No Threat Detected:** Test this result by scanning any file you are certain is clean (e.g., a newly created text file)
- **Infected/Known :**

  1. Download an EICAR test file from [here](https://www.eicar.org/download-anti-malware-testfile/).
  2. Scan the file.
- **Suspicious :** This result is usually caused by an engine's heuristic algorithm. (We can actually simulate to produce this result if we write a script with external scanner.)
- **Blocklisted :** Test this result by adding the file to be tested to the **Blocklist**. For instructions on how to add files to the **Blocklist**, please refer to the [Workflow Configuration Template](/docs/mdcore/configuration/workflow-configuration-template)**.**
- **Allowlisted:** Test this result by adding a file by its name or its mime-type to the **Skip** option and then scanning it. For more instructions on how to **Allowlist** files, please refer to the [Workflow Configuration Template](/docs/mdcore/configuration/workflow-configuration-template)**.**
- **Exceeded Archive Size :**

  1. Configure **"Max total size of extracted files"** to a small value (i.e. 5 MB). This setting can be found on the MetaDefender Core Management Console under Policies→Workflow Rules→Select Workflow Rule→Archive Tab.
  2. Create an archive file with a total size greater than 5 MB (after extraction).
  3. Scan the file.
- **Exceeded Archive File Number :**

  1. Configure **"Max number of files extracted"** with a small value (i.e. 10). This setting can be found on the MetaDefender Core Management Console under Policies→Workflow Rules→Select Workflow Rule→Archive Tab.
  2. Create an archive file that contains more than 10 files (after extraction).
  3. Scan the file.
- **Password encrypted document/archive:** Scanning a password protected/encrypted document will produce this result. Currently, ● MetaDefender Core supports decryption of encrypted files both directly via the **Management Console** (as illustrated below) and via **REST API**.

- **Exceeded Archive Depth:** Test this result by configuring a lower recursion level than the current archive depth settings (Policies→Workflow Rules→Select Workflow Rule→Archive Tab)
- **Failed to scan:** Test this result by sending a file to scan which has no read permissions or is invalid. Alternatively, if no engine is in the MetaDefender Core installation and scan is enabled through the Security Rule configurations, this will be the final result
- **Mismatch:**

  1. Test this result by enabling the **"Detect File Type Mismatch"** option from the **"Policies",** tab **"File Type Analysis"** under the section inside of the **"Workflow Rule"** you are using.
  2. Alternatively, this result can be tested by changing the original extension of a file to different extension (i.e. test.docx → test.pdf) and scanning the file.
  3. Note that the option **"Detect File Type Mismatch"** only applies to workflows.
- **Potentially Vulnerable File:** Clean files can be marked as vulnerable if the Vulnerability Engine identifies known application vulnerabilities which are then reported by severity level. For more information on the **Vulnerability Engine**, please refer [here](https://www.opswat.com/technologies/vulnerability-assessment)

Support:

If you have any difficulty running tests to view scan results on MetaDefender Core, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
