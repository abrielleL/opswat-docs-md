<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/webhook -->

# Webhook

| Last Update | 24 Mar 2020 |
| ---- | ---- |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Response Format | JSON |
| Requirements | Only applicable for enterprise accounts |
| Changes |  |

My OPSWAT Central Management now supports webhook to allow an account to push a notification to a 3rd-party vendor when an event is triggered. The 3rd party vendor can leverage this feature to continuously monitor device compliance status while a device is connecting to a protected resources/applications.

## Configuration

An administrator can enable this feature by following the below steps

- Log into My OPSWAT Central Management console
- Navigate to** Settings > Integrations**
- On the Webhook tab,
  - Enter a callback API which you would like My OPSWAT Central Management push a notification to
  - Enter an API Key to authenticate with the callback API server
  - Check on events to trigger a notification.

![](https://image-archive.developerhub.io/image/upload/v2_5265/aazh9ezcbbjeocfxzhze/1628792203.png)

**Warning:**

- This feature will be auto-disabled if My OPSWAT Central Management could not reach out to a configured callback API. Administrators need to log into My OPSWAT Central Management console and enable this feature manually in that case.

## Callback API Definition

## API URL

```plaintext
POST URL HTTP/1.1
```

## Request Header

| Key | Value | Description |
| ---- | ---- | ---- |
| Content-Type | application/json |  |
| Authorization | API Key value | 3rd party vendor needs to issue an API key for authentication purpose |

## Request Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| device_id | string | Device ID |
| status | string | device status Values can be: - "compliant": A device changes status to compliant - "non_compliant": A d evice changes status to non- compliant - "installed": A device installed  MetaDefender Endpoint - " deleted ": A device was removed from the account. This can happen when   - a device is deleted by an administrator from console or through an API action.   - a user uninstalled the  MetaDefender Endpoint on the device ***Note: this can be extended in future*** |
| timestamp | long | Timestamp when an even is triggered (Unix timestamps in milliseconds) |

## Response Code

| HTTP Code | Description |
| ---- | ---- |
| 2xx For example: 200, 202 | Successful |
| other codes | Failed My OPSWAT Central Management will retry 2 times after 4 seconds and 1 min. And My OPSWAT Central Management will auto-disable the Webhook settings if it fails 100 consecutive pushes |

## Example Request

```plaintext
POST https://your-callback-url
HEADER:
Content-Type: application/json
Authorization: 5c61d579ad574298cf00dbdd83d584c6
 
BODY:
[{
	"device_id": "6WXJURV8QAM0I7KC",
	"status": "compliant",
	"timestamp": 1582708254594
}]
```

## Example Response successful (HTTP 2xx)

```plaintext
HTTP 200 ok
```

## Example Response failed (HTTP code is not equal 2xx)

```plaintext
HTTP 500
```

## Logs

My OPSWAT Central Management records an event log when it pushes a notification to a configured callback API with a HTTP status code from the API. Administrators can check event logs for this feature at Event Log > Webhook
