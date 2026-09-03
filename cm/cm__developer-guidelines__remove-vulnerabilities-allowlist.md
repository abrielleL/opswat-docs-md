<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/remove-vulnerabilities-allowlist -->

# Remove Vulnerabilities Allowlist

| API version | 3.0 |
| ---- | ---- |
| Last Update | 05/07/2026 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Change History | Add support for removing Vulnerabilities Allowlist settings |

## API URL

```plaintext
https://gears.opswat.com/o/api/v3/cves/allowlist/delete
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | Access token which archived from OAuth authentication step |  |
| cve_ids | string array | Body | Yes | Non-empty list (max 100) of CVE IDs to remove from the allowlist. Each must exist in the CVE database. |  |

## Response HTTP Code

Refer to [APIs](https://www.opswat.com/docs/cm/developer-guidelines/apis) page for more details.

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| (no body) |  | On success (HTTP 200), the response body is empty. |

## Example

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v3/cves/allowlist/delete?access_token=XXXXXXXXXXXXXXXXXXXXXXXXXXXXX
{
    "cve_ids": ["CVE-2021-44228", "CVE-2022-0778"]
}
```

**Example Response**

```plaintext
HTTP 200 OK
```
