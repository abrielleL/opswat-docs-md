<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/update-policy-blocklist-cve -->

# Update Policy Blocklist CVE

| API version | 1.0 |
| ---- | ---- |
| Last Update | 05/07/2026 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Change History | Add support for updating Policy Blocklist CVE |

## API URL

```plaintext
https://gears.opswat.com/o/api/v1/policies/:policy_id/block_cves/update
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | Access token which archived from OAuth authentication step |  |
| policy_id | string | URL | Yes | ID of the policy |  |
| os | string | Body | Yes | Operating system. One of: `windows`, `macos`, `linux` |  |
| cves | string[] | Body | Yes | CVE IDs to set. Must not be null or empty. Max 10000 items. |  |

## Response HTTP Code

Refer to [APIs](https://www.opswat.com/docs/cm/developer-guidelines/apis) page for more details.

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| invalid_cves | string[] | Optional. List of CVE IDs that were not valid. Present only when some CVEs in the request are invalid. |

## Example

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v1/policies/:policy_id/block_cves/update?access_token=XXXXXXXXXXXXXXXXXXXXXXXXXXXXX
{
    "os": "windows",
    "cves": ["CVE-2021-44228", "CVE-2022-0778"]
}
```

**Example Response** **(all valid)**

```plaintext
HTTP 200 OK
```

**Example Response (some invalid)**

```plaintext
{
    "invalid_cves": ["CVE-INVALID-1"]
}
```
