<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/event-based-real-time-handling-for-oraclesdk -->

# Event-Based Real-Time handling for OracleSDK

## Oracle Rule with custom Function trigger Setup Guide

This guide explains how to configure **Oracle Cloud Functions** and **Object Storage Events** to enable **real-time event-based processing** in MetaDefender Storage Security (MDSS) when using the **Oracle Native SDK** integration.

## Prerequisites

Before proceeding with the setup, ensure the following requirements are met.

### 1. Required Permissions

Your Oracle Cloud Infrastructure (OCI) environment only needs the following **IAM permissions** **if you plan to deploy the function from an OCI repository**. Deploying from the repository is optional; these permissions are **not required** if you use other deployment methods.

| **Dynamic Group Permissions** |
| ---- |
| Allow dynamic-group <your_dynamic_ group> to to read repos in tenancy |
| Allow dynamic-group <your_dynamic_ group> to use repos in tenancy |

These permissions enable your function to **read and execute code from the OCI repository**.

### 2. Network and Access Requirements

- The function’s subnet must allow outbound access to the public MDSS domain. No specific protocol (HTTP/HTTPS) is enforced by MDSS.
- Ensure your **Object Storage bucket** is in the same **tenancy and region** as your Function Application (recommended for lower latency).
- Verify that your **Object Storage bucket emits object events** (see Step 5).

## Step 1: Create an Application and Function

1. In the Oracle Cloud Console, navigate to **Developer Services → Functions → Applications**.
2. Click **Create Application** and provide:
   - **Name**: e.g. `MetaDefenderStorageProcessorApp`
   - **VCN/Subnet**: Select a subnet with outbound internet access.
3. Once created, open your application and click **Create Function**.
4. Set:
   - **Function Name**: `MetaDefenderStorageSecurityProcessor`
   - **Runtime**: **Python**
   - **Entry Point**: `handler`

You can create and deploy your function either from the **OCI Console Code Editor** or using the **OCI CLI / Fn Project CLI**.

## Step 2: Implement Function Code

Use the following Python function implementation. This code listens to Object Storage create events and sends real-time metadata to your MDSS instance for processing.

```python
import io
import os
import json
import urllib.request
from urllib.parse import unquote
from fdk import response

def handler(ctx, data: io.BytesIO = None):
    event_body = json.loads(data.getvalue())
    object_key = event_body.get('data', {}).get('resourceName', '')
    object_key = unquote(object_key.replace("+", " "))

    payload = {
        "metadata": json.dumps({"Name": object_key}),
        "storageClientId": os.getenv("STORAGECLIENTID", "")
    }

    req = urllib.request.Request(
        url=os.getenv("APIENDPOINT", ""),
        data=json.dumps(payload).encode("utf-8"),
        headers={
            "ApiKey": os.getenv("APIKEY", ""),
            "Content-Type": "application/json"
        },
        method="POST"
    )

    urllib.request.urlopen(req, timeout=5)

    return response.Response(
        ctx,
        response_data=json.dumps({"status": "ok"}),
        headers={"Content-Type": "application/json"}
    )
```

## Step 3: Configure Function Environment Variables

1. Open your **Function details** page in the Oracle Cloud Console.
2. Click **Configuration → Environment Variables → Edit**.
3. Add the following key-value pairs:

| Key | Value | Description |
| ---- | ---- | ---- |
| APIENDPOINT | Your MDSS URL + `/api/webhook/realtime` | The MDSS real-time processing API endpoint |
| APIKEY | Your MDSS user API key | Your MDSS API key with webhook permissions |
| STORAGECLIENTID | Your storage client ID from MDSS | Navigate to your desired storage configuration and copy the `storageClientId`  in order to obtain |

4. Click **Save Changes**.

## Step 4: Deploy the Function

If you are using the Code Editor in the OCI Console, click **Deploy**.

If you are using the CLI:

```bash
fn deploy --app MetaDefenderStorageProcessorApp
```

Once deployment completes, confirm your function appears in the **Functions** list and has an active **endpoint**.

## Step 5: Create Object Storage Rule and Enable Event Emission

You will now link your Object Storage bucket to your Oracle Function so that MDSS receives file events in real time.

### 5.1 Create a Rule

1. In the OCI Console, navigate to **Observability & Management → Events Service → Rules**.
2. Click **Create Rule** and configure:
   - **Name**: `ObjectCreateTriggerRule`
   - **Condition**:
     - **Service**: *Object Storage*
     - **Event Type**: *Object - Create*
   - **Actions**:
     - Select **Functions** and choose your **MetaDefenderStorageSecurityProcessor** function.
3. Click **Create Rule**.

This ensures that every time a new object is created in your bucket, an event triggers the Function.

### 5.2 Enable Object Event Emission on the Bucket

1. Navigate to **Object Storage → Buckets → [Your Bucket Name]**.
2. Under **Events**, click **Emit Object Events** → **Enable**.
3. Save your configuration.

## Step 6: Testing and Validation

1. Upload a new file to your configured **Object Storage bucket**.
2. Open the **Functions → Metrics & Logs** tab to confirm the function execution was triggered.
3. Check the **MDSS instance** to verify the event was received and the file processing started.
4. If successful, the MDSS dashboard should show the new file scan in progress.

## Request and Response Format

**Request Body (Example)**

```json
{
    "storageClientId": "{Storage Client Id}",
    "metadata": "{'Name': 'uploads/sample.pdf'}"
}
```

**Successful Response Example**

```json
{
    "correlationId": "67ea85a36f2f5732a82834d0"
}
```

| Field | Description |
| ---- | ---- |
| correlationId | A unique identifier that references the submitted file in our database. You can use this ID for tracking the file's processing status or for future API calls related to this file. |

#### Error

When an error occurs during processing, the system returns:

```json
{
    "responseKey": "REST_API_MSG_FAILED_STORAGE_RTP_NOT_ENABLED",
    "responseMessage": "Real-Time Process is not enabled."
}
```

| Field | Description |
| ---- | ---- |
| responseKey | Machine-readable error code that identifies the specific error condition. |
| responseMessage | Human-readable explanation of the error. |

#### Common error responses

| Response Message | Description | Recommended Action |
| ---- | ---- | ---- |
| The storage could not be found | The specified storage client ID does not exist in the system. | Verify the storageClientId is correct and the storage has been properly configured in the system. |
| Real-Time Process is not enabled. | Real-time processing has not been activated for this storage client. | Enable real-time processing for the storage client in your account settings. |
| Real-Time Process is enabled, but it is not set to Event Based. | The storage is configured for real-time processing, but is using polling rather than event-based processing. | Stop the current RTP scan and start another one using Event-Based |

## Summary

After completing this setup:

- Oracle **Object Storage** emits events on object creation.
- **Oracle Cloud Function** receives the event and forwards it to **MDSS** via webhook.
- **MDSS** immediately begins scanning the uploaded object in real time.

This configuration enables secure, low-latency, event-driven protection for files stored in Oracle Object Storage.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
