<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/will-mft-pull-job-retrieve-incomplete-files-via-sftp- -->

# Will MFT Pull Job Retrieve Incomplete Files via SFTP?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article applies to all MetaDefender MFT Version releases deployed on Window/Linux.

### [Summary](/docs/mdmft/knowledge-base/will-mft-pull-job-retrieve-incomplete-files-via-sftp-#summary)

When performing a **PULL** action in OPSWAT MFT, the process may sometimes stop unexpectedly. This document explains whether MFT retrieves incomplete files during such transfers.

#### [Use case](/docs/mdmft/knowledge-base/will-mft-pull-job-retrieve-incomplete-files-via-sftp-#use-case)

During an active MFT job, MFT first verifies and accumulates the file size before initiating the transfer process.

In this test, three file types were used:

- `light_test`
- `medium_test`
- `heavy_test`

### [**Test File Execution**](/docs/mdmft/knowledge-base/will-mft-pull-job-retrieve-incomplete-files-via-sftp-#test-file-execution)

**Example:** A successful PULL action

- **Job Logs:** Show standard processing with no interruption
- **Processing Status:** Completed
- **Final Status:** Success

JOB logs

Processing status

Final status

#### [**Issue – Scenario 1: Job Interrupted**](/docs/mdmft/knowledge-base/will-mft-pull-job-retrieve-incomplete-files-via-sftp-#issue--scenario-1-job-interrupted)

In cases where the job is interrupted or disconnected unexpectedly during execution, the file transfer is aborted.

- **Result:** No files are received by MFT.
- **Error Logs:** Indicate termination or connection failure.

Error logs

#### [**Issue – Scenario 2: File Still Being Written**](/docs/mdmft/knowledge-base/will-mft-pull-job-retrieve-incomplete-files-via-sftp-#issue--scenario-2-file-still-being-written)

When a file is still being written to (e.g., ongoing upload to SFTP), MFT detects it as **incomplete** or **in use**.

- **Result:** MFT will **not retrieve** the file. Only fully written, unmodified files are pulled.
- **Job Logs:** Reflect skipped or untransferred files.

JOB logs

Warning:

In this scenario **INCOMPLETE** file will not be retrieved. And only unmodified files are pulled to MFT

Support:

If you have followed all of the steps above but are still unable to resolve the issue. Please follow these instructions on [Creating Support Packages - MetaDefender Managed File Transfer](https://www.opswat.com/docs/mdmft/troubleshooting/how-to-create-support-package) before [creating a support case or chatting with our support engineer.](https://my.opswat.com/support)
