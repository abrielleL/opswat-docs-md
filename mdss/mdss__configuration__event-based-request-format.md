<!-- source: https://www.opswat.com/docs/mdss/configuration/event-based-request-format -->

# Event-Based request format

## [Overview](/docs/mdss/configuration/event-based-request-format#overview)

This document describes the real-time webhook API endpoint that external integrators can use to notify the system about file events. The endpoint accepts different payload formats depending on the storage type.

## [Endpoint Information](/docs/mdss/configuration/event-based-request-format#endpoint-information)

**URL:** `https://{baseurl}/api/webhook/realtime`

**Method:** POST

**Content-Type:** application/json

Important note for Box integration

For Box, the API endpoint is **https://{baseurl}/api/webhook/realtime/public/{storageClientId}.** Please refer to [this article](/docs/mdss/configuration/event-based-handling-for-box) for specific instructions.

## [Request Format (with examples)](/docs/mdss/configuration/event-based-request-format#request-format-with-examples)

The request body differs based on storage type. Below are the specifications for each supported storage:

#### [Amazon S3 and S3 Compatible](/docs/mdss/configuration/event-based-request-format#amazon-s3-and-s3-compatible)

FormatExample (file in root)Example (file in nested directory)Copy{
"metadata": "{\"s3\": { \"object\": {\"key\": \"{Object Path}\" }}}",
"storageClientId": "{Storage Client Id}"
}{
"storageClientId": "0c5454e3-d576-44c5-8ce4-cdc078011d0b",
"metadata": "{\"s3\": { \"object\": {\"key\": \"test-file.txt\" }}}"
}{
"storageClientId": "0c5454e3-d576-44c5-8ce4-cdc078011d0b",
"metadata": "{\"s3\": { \"object\": {\"key\": \"folder1/folder2/test-file.txt\" }}}"
}
#### [Alibaba Cloud](/docs/mdss/configuration/event-based-request-format#alibaba-cloud)

FormatExample (file in root)Example (file in nested directory)Copy{
"metadata": "{\"oss\": {\"object\": {\"key\": \"{Object Path}\"}}}",
"storageClientId": "{Storage Client ID}"
}{
"metadata": "{\"oss\": {\"object\": {\"key\": \"test-file.pdf\"}}}",
"storageClientId": "0c5454e3-d576-44c5-8ce4-cdc078011d0b"
}{
"metadata": "{\"oss\": {\"object\": {\"key\": \"folder1/folder2/test-file.pdf\"}}}",
"storageClientId": "0c5454e3-d576-44c5-8ce4-cdc078011d0b"
}
#### [Google Cloud, OracleSdk, Azure Blob, SMB Compatible, NFS, SFTP, FTP and NetApp ONTAP](/docs/mdss/configuration/event-based-request-format#google-cloud-oraclesdk-azure-blob-smb-compatible-nfs-sftp-ftp-and-netapp-ontap)

FormatExample (file in root)Example (file in nested directory)Copy{
"metadata": "{\"Name\": \"{Object Path}\" }",
"storageClientId": \"{Storage Client ID}\"
}{
"metadata": "{\"Name\": \"test-file.exe\" }",
"storageClientId": "0c5454e3-d576-44c5-8ce4-cdc078011d0b"
}{
"metadata": "{\"Name\": \"folder1/folder2/test-file.exe\" }",
"storageClientId": \"0c5454e3-d576-44c5-8ce4-cdc078011d0b\"
}
### [Scanning with a partition](/docs/mdss/configuration/event-based-request-format#scanning-with-a-partition)

If you have one or more partition Event-Based scans active, a new parameter called `scanId` is required with every request and the format will become:

JsonCopy{
"metadata": "{Metadata format specific for every storage}",
"storageClientId": \"{Storage Client ID}\",
"scanId": "Scan Id for the scan with partition"
}
##

## [Response Formats](/docs/mdss/configuration/event-based-request-format#response-formats)

#### [Success](/docs/mdss/configuration/event-based-request-format#success)

When a webhook is successfully processed, the system returns:

Success response exampleCopy{
"correlationId": "67ea85a36f2f5732a82834d0"
}

| Field | Description |
| --- | --- |
| correlationId | A unique identifier that references the submitted file in our database. You can use this ID for tracking the file's processing status or for future API calls related to this file. |

#### [Error](/docs/mdss/configuration/event-based-request-format#error)

When an error occurs during processing, the system returns:

Error response exampleCopy{
"responseKey": "REST_API_MSG_FAILED_STORAGE_RTP_NOT_ENABLED",
"responseMessage": "Real-Time Process is not enabled."
}

| Field | Description |
| --- | --- |
| responseKey | Machine-readable error code that identifies the specific error condition. |
| responseMessage | Human-readable explanation of the error. |

#### [Common error responses](/docs/mdss/configuration/event-based-request-format#common-error-responses)

| Response Message | Description | Recommended Action |
| --- | --- | --- |
| The storage could not be found | The specified storage client ID does not exist in the system. | Verify the storageClientId is correct and the storage has been properly configured in the system. |
| Real-Time Process is not enabled. | Real-time processing has not been activated for this storage client. | Enable real-time processing for the storage client in your account settings. |
| Real-Time Process is enabled, but it is not set to Event Based. | The storage is configured for real-time processing, but is using polling rather than event-based processing. | Stop the current RTP scan and start another one using Event-Based |
