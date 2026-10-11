<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/file-scanned-notifications -->

# File scanned notifications

## Overview

File Scanned webhook notifications allow you to receive real-time alerts whenever a file has been scanned by MetaDefender Storage Security. This feature is useful if you need to:

- Track the outcome of file scans for auditing or compliance.
- Integrate scan results into external systems (e.g., ticketing, alerting, SIEM).
- Trigger automated workflows based on file status (e.g., quarantine, user notification).

## Setup

1. Go to **Settings** **> Notifications** in the MetaDefender Storage Security console.
2. Select **Upon File Scan** under the **Webhook Notifications** section
3. Choose whether you want to receive notifications for **all scanned files** or **only blocked files**.
4. Enter the **Destination Address** (your endpoint).
5. Select the **Request Type** (**POST** or **PUT**).
6. (Optional) Add any custom **HTTP headers**.
7. Save the configuration.

![](https://uploads.developerhub.io/prod/k8zL/8w5ir0hoopdl1casd271wtqv3i5eno8veytwzaih3kej29n29aykwwufdh4ebzrz.png)

## Configuration Details

- **Destination address** – The URL of the receiving system (must accept HTTP requests).
- **Request type** – Either `POST` or `PUT`.
- **Headers** – Optional key-value pairs (e.g., `Authorization: Bearer <token>`).
- **Notification scope** – Choose between:
  - **All scanned files** → You will receive a notification for every file scanned.
  - **Blocked only** → You will only receive notifications when a file is marked as blocked in MetaDefender Storage Security (see [File Definition](https://www.opswat.com/docs/mdss/configuration/file-definition))

## Webhook Payload

When triggered, the webhook sends a JSON request body to your configured endpoint.

```json
{
  "FileId": "0198f02f-ed4d-7c0d-8668-1036d322209c",
  "FileName": "file.txt",
  "FilePath": "folder/file.txt",
  "FileStatus": "Allowed",
  "CoreScanResult": "No Threat Detected",
  "FileState": "Available",
  "RemediationResult": [
    "AllowedKept: Applied"
  ],
  "ScanCompletedTimeStamp": "2025-08-28T10:20:24.974998Z",
  "WorkflowName": "Default Workflow",
  "Rules": [
    "MetaDefender Storage Security"
  ],
  "ExceptionDetails": "",
  "RemediationErrors": [],
  "WebhookNotificationType": "FileScanned"
}
```

### Field Reference

| Field | Type | Example Value | Description |
| ---- | ---- | ---- | ---- |
| `FileId` | string (UUID) | `0198f02f-ed4d-7c0d-8668-1036d322209c` | Unique identifier of the file. |
| `FileName` | string | `file.txt` | Original file name. |
| `FilePath` | string | `folder/file.txt` | File's relative path. |
| `FileStatus` | string | `Allowed` /`Blocked` | File status based on MDSS file definitions |
| `CoreScanResult` | string | `No Threat Detected` | Result from Scan instance. |
| `FileState` | string | `Failed` / `Canceled` / `FailedRemediation` / Available | File status in MDSS. |
| `RemediationResult` | array[string] | `["AllowedKept: Applied"]` | Array of remediations applied and their result |
| `ScanCompletedTimeStamp` | datetime (UTC) | `2025-08-28T10:20:24.974998Z` | Time when scan completed. |
| `WorkflowName` | string | `Default Workflow` | Name of the workflow used. |
| `Rules` | array[string] | `["MetaDefender Storage Security"]` | Workflow rules applied. |
| `ExceptionDetails` | string | "" | Details of any exceptions during scan. |
| `RemediationErrors` | array[string] | `[]` | Errors during remediation, if any. |
| `WebhookNotificationType` | string | `FileScanned` | Identifies the notification type. |

## Delivery Behavior

- Webhooks are delivered as standard HTTP requests.
- Delivery is **best-effort** → if the destination is invalid, the request is logged in the **Audit page**, but **no retries** are performed.
- Payload size is typically small (JSON only, no file contents).

## Security Considerations

- Configure HTTPS endpoints to ensure data is transmitted securely.
- Use authentication headers (e.g., API tokens) to protect your webhook endpoint.
- Ensure your endpoint validates payloads before processing.

## Troubleshooting

- **No webhook received** → Verify the endpoint URL and request type (POST/PUT).
- **Audit shows delivery failed** → Endpoint is invalid. Fix and test again.
- **Authentication errors** → Confirm your endpoint accepts the headers you configured.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
