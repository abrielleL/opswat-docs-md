<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/update-vulnerabilities-allowlist -->

# Update Vulnerabilities Allowlist

| API version | 3.0 |
| ---- | ---- |
| Last Update | 05/07/2026 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Change History | Add support for updating Vulnerabilities Allowlist settings |

## API URL

```plaintext
https://gears.opswat.com/o/api/v3/cves/allowlist/update
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | Access token which archived from OAuth authentication step |  |
| cve_ids | string array | Body | Yes | Non-empty list of CVE IDs to add to the allowlist. Each must exist in the CVE database. Max 100 items. |  |
| allowlisted_by_all_policies | boolean | Body | Yes | Apply allowlist to every policy in the account. When set to `true`, `allowlisted_by_specific_policies`, `allowlisted_by_specific_devices`, `policy_ids`, and `device_ids` are ignored. When `false`, at least one of `allowlisted_by_specific_policies` or `allowlisted_by_specific_devices` must be `true`. |  |
| allowlisted_by_specific_policies | boolean | Body | Yes | Enable when allowlisting at the policy level. When `true` and `allowlisted_by_all_policies=false`, `policy_ids` must be provided. |  |
| allowlisted_by_specific_devices | boolean | Body | Yes | Enable when allowlisting at the device level. When `true` and `allowlisted_by_all_policies=false`, `device_ids` must be provided. |  |
| policy_ids | string array | Body | Conditional | List of policy IDs to allowlist the CVEs for. Required when `allowlisted_by_all_policies=false` and `allowlisted_by_specific_policies=true`. Max 100 items. |  |
| device_ids | string array | Body | Conditional | List of device IDs to allowlist the CVEs for. Required when `allowlisted_by_all_policies=false` and `allowlisted_by_specific_devices=true`. Max 500 items. |  |

## Response HTTP Code

Refer to [APIs](https://www.opswat.com/docs/cm/developer-guidelines/apis) page for more details.

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| (no body) |  | On success (HTTP 200), the response body is empty. |

## Example

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v3/cves/allowlist/update?access_token=XXXXXXXXXXXXXXXXXXXXXXXXXXXXX
{
    "cve_ids": ["CVE-2021-44228", "CVE-2022-0778"],
    "allowlisted_by_all_policies": false,
    "allowlisted_by_specific_policies": true,
    "allowlisted_by_specific_devices": false,
    "policy_ids": ["policy_id"],
    "device_ids": ["device_id"]
}
```

**Example Response**

```plaintext
HTTP 200 OK
```
