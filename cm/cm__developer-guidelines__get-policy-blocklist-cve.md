<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-policy-blocklist-cve -->

# Get Policy Blocklist CVE

| API version | 1.0 |
| ---- | ---- |
| Last Update | 05/07/2026 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Change History | Add support for getting Policy Blocklist CVEs |

## API URL

```plaintext
https://gears.opswat.com/o/api/v1/policies/:policy_id/block_cves
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | Access token which archived from OAuth authentication step |  |
| policy_id | string | URL | Yes | ID of the policy |  |
| os | string | Body | Yes | Operating system. One of: `windows`, `macos`, `linux` |  |

## Response HTTP Code

Refer to [APIs](https://www.opswat.com/docs/cm/developer-guidelines/apis) page for more details.

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| cves | string array | List of CVE IDs in the blocklist for the specified OS. Return empty if no blocklist is set. |

## Example

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v1/policies/:policy_id/block_cves?access_token=XXXXXXXXXXXXXXXXXXXXXXXXXXXXX
{
    "os": "windows"
}
```

**Example Response**

```plaintext
{
    "cves": ["CVE-2021-44228", "CVE-2022-0778"]
}
```
