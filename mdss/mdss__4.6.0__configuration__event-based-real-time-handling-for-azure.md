<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/event-based-real-time-handling-for-azure -->

# Event-Based Real-Time handling for Azure

## Azure Blob function app setup

1. Deploy the Azure function app using the Terraform script: [https://github.com/OPSWAT/metadefender-k8s/tree/main/terraform/azure-function-docker](https://github.com/OPSWAT/metadefender-k8s/tree/main/terraform/azure-function-docker)
2. Configure `STORAGECLIENTID`, `APIKEY`, and `APIENDPOINT` variables in the `.tvars` file:

```python
resource_group_name = "" #The name of the resource group in which the function app will be created."
service_plan_name = "" #The name of the app service plan
storage_account_name = "" #The name of the storage account to be created
docker_registry_server_url = ""
docker_registry_server_username = "" #optional
docker_registry_server_password = "" #optional
docker_image_name = ""
docker_image_tag = ""
AzureWebJobsBlobTrigger = "" #The storage account connection string that triggers the function
CONTAINERNAME = "" #The blob container that needs to be scanned
fn_name_prefix = "" #function name
location = "" #azure region
STORAGECLIENTID  = ""
APIKEY = ""
APIENDPOINT = ""
```

## Request Format (with examples)

The request body differs based on storage type. Below are the specifications for each supported storage:

#### Amazon S3 and S3 Compatible

```json
{
    "storageClientId": '{Storage Client Id}',
    "metadata": "{'s3': { 'object': {'key': '{Object Path}' }}}"
}
```

```json
{
    "storageClientId": "0c5454e3-d576-44c5-8ce4-cdc078011d0b",
    "metadata": "{'s3': { 'object': {'key': 'test-file.txt' }}}"
}
```

```json
{
    "storageClientId": "0c5454e3-d576-44c5-8ce4-cdc078011d0b",
    "metadata": "{'s3': { 'object': {'key': 'folder1/folder2/test-file.txt' }}}"
}
```

## Response Formats

#### Success

When a webhook is successfully processed, the system returns:

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

### Azure Blob Event Grid RTP configuration

Refer to the example for detailed configuration: [https://github.com/OPSWAT/metadefender-k8s/tree/main/terraform/CloudFunctions/Azure/webhook-notification](https://github.com/OPSWAT/metadefender-k8s/tree/main/terraform/CloudFunctions/Azure/webhook-notification)

> **WARNING**
>
> Event Notifications for Page and Append blob are **NOT** supported.
>
> Events for these blob types are triggered upon the first block commit, potentially before the upload is complete.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
