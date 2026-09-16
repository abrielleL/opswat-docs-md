<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-rest-api-file-submission-with-downloadfrom-header-fails-when -->

# Why REST API File Submission with downloadfrom Header Fails When Using RAMDISK for Temp Directory?

**Check Your Version:** This article applies to all MetaDefender Core releases deployed on Windows and Linux systems after 5.11.1.

## [**Issue:**](/docs/mdcore/v5.22.0/knowledge-base/why-rest-api-file-submission-with-downloadfrom-header-fails-when#issue)

When configuring a RAMDISK as the temporary directory using IMDisk, file submissions through the browser interface function correctly; however, submissions via the REST API fail due to issues with the `downloadfrom` header.

### [**Error Details:**](/docs/mdcore/v5.22.0/knowledge-base/why-rest-api-file-submission-with-downloadfrom-header-fails-when#error-details)

The following error is logged:

> [WARNING] 2025.11.03 20:50:22.994: (common.workflow) Workflow block ended with exception, block='ErrorRestResponse', workflow_id='', error='Cannot send message to Frontend' [msgid: 97]

You may encounter the message 'Cannot send message to Frontend' in `core.log`, while the REST API request returns an error: `“err”: “File download rejected due to insufficient disk space”`.

## [**Resolution:**](/docs/mdcore/v5.22.0/knowledge-base/why-rest-api-file-submission-with-downloadfrom-header-fails-when#resolution)

Until a fix is available, consider using a physical disk path for the temporary directory instead of a RAMDISK when submitting files via the REST API with the `downloadfrom` header.

 **Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
