<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-do-some-multipart-uploads-fail-with-error-code-500- -->

# Why do some multipart uploads fail with error code 500?

This article applies to MetaDefender Core releases versions 5.17.1 and earlier deployed on Windows and Linux systems.

1. Issue description

When uploading large files via API, using /file/multipart requests with chunks that are multiple of 1MB, those chunks fail with error code 500.

2. Steps to confirm issue

In the custom script used to split the uploaded file in to chunks, verify the configured size for the split chunks. The upload fails when the chunk size is a multiple of exactly 1MB (i.e. 1MB, 7MB, 20MB etc).

The Core logs output a [WARNING] containing (core.workflow) Empty data chunk received, stop data transfer and NGINX shows a code 500 response for the upload.

3. Solution

The correct and persistent fix is udpating MetaDefender Core to version 5.18.0 or later.

4. Workaround

If updating MetaDefender is not feasible at the time, a temporary workaround is adapting the uploading script to split the files in chunks that are not equal to a multiple of 1MB, for example adding or substracting 1KB from the chunk size.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
