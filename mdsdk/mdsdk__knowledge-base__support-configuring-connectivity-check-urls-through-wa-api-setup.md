<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup -->

# Support configuring connectivity check URLs through wa_api_setup

This article applies to OESIS Framework version **4.3.5778.0** and later on Windows, **4.3.5219.0** and later on macOS, and **4.3.4820.0** and later on Linux.

## [**Overview**](/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup#overview)

OESIS validates whether a device has network/internet connectivity before running certain operations, such as security checks that must communicate with a cloud service.

By default, OESIS performs this validation by sending an HTTP/HTTPS request to a fixed public URL: `http://www.google.com`.

In some environments, this default behavior is not acceptable or does not work, for example:

- **Strict security policies** Outbound connections to public websites like `google.com` may be blocked by corporate policy or by country‑level controls.
- **Isolated / air‑gapped environments** Systems may have no direct internet access; only internal network resources (intranet) are reachable.
- **Segmented networks** Traffic may only be allowed to specific internal or approved external endpoints.

In these cases, customers:

- Do **not** want the SDK to contact `google.com`, and
- Want to use **their own approved endpoints** (for connectivity checks to internet or intranet) instead.

This article describes how to configure custom URLs or IP addresses for connectivity checks, while preserving the current default behavior for customers who do not configure anything. **

## [**How connectivity checks work**](/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup#how-connectivity-checks-work)

When checking connectivity, OESIS sends **HTTP GET** requests (over HTTP or HTTPS) to each configured endpoint (URL or IP address, optionally with a port).

A connectivity check is considered **successful** when:

- A TCP connection to the endpoint can be established, and
- Any HTTP response is received within the SDK’s timeout window.

HTTP status codes are interpreted as follows:

- **2xx** responses are treated as **successful**.
- **Non‑2xx** responses still indicate that the endpoint is **reachable**; higher‑level logic may interpret these codes as needed.

Connectivity checks typically run:

- Before operations that require internet/cloud access (for example, startup readiness checks or on‑demand validations before cloud calls).
- Whenever the application explicitly triggers a connectivity verification.

If no custom endpoints are configured, OESIS continues to use the default public URL `http://www.google.com`. **

## [**Configuration in wa_api_setup**](/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup#configuration-in-wa_api_setup)

### [High‑level behavior](/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup#highlevel-behavior)

A new optional configuration object, `connectivity_check`, is available under `config` in `wa_api_setup`.

- If `config.connectivity_check.global_urls` is **set**: OESIS performs connectivity checks **only** against the URLs/IPs in that list.
- If `config.connectivity_check.global_urls` is **not set**: OESIS keeps the current behavior and uses the default public URL `http://www.google.com`.

### [JSON configuration example](/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup#json-configuration-example)

JsonCopy{
"config": {
"connectivity_check": {
"global_urls": [
"https://www.google.com",
"127.0.0.1:3000"
]
}
}
}
### [Field details](/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup#field-details)

- `connectivity_check` (object, optional): Container object for connectivity‑related settings.
- `connectivity_check.global_urls` (array of strings, optional): A list of endpoints that OESIS will use to check connectivity. Behavior:

  - When this option is set, OESIS **replaces** the default public URL and uses **only** the endpoints in this list.
  - If no port is specified:

    - For `http://` URLs and bare IPs, OESIS uses port **80**.
    - For `https://` URLs, OESIS uses port **443**.

Note on multiple elements

When multiple endpoints are listed in `global_urls`, OESIS sends HTTP requests to **all** of them in parallel. If at least one endpoint is reachable (under the rules described above), the connectivity check is considered successful.

### [Accepted formats](/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup#accepted-formats)

The `global_urls` array accepts the following endpoint formats:

- **HTTP/HTTPS URLs**

  - Example:

    - `https://internettest.com`
    - `http://intranet.check.local:8080`
- **IP addresses (IPv4 or IPv6), with or without port numbers**

  - Examples:

    - `10.0.0.5`
    - `192.168.10.20:8080`
    - `[2001:db8::1]`

This allows you to:

- Point checks to a **whitelisted external URL** (for example, `https://internettest.com`), or
- Use an **internal service** (intranet endpoint) to represent “connectivity is available”, including in air‑gapped or restricted environments.

## [**Validation and error codes**](/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup#validation-and-error-codes)

During `wa_api_setup`, OESIS validates the structure and types of the `connectivity_check` configuration.

If the configuration is invalid, one of the following error codes may be returned:

| Error Name | ID | When it is returned | Example of invalid config |
| --- | --- | --- | --- |
| `WAAPI_ERROR_CONFIG_INVALID_CONNECTIVITY_CHECK_TYPE` | -90 | `config.connectivity_check` exists but is not an object | `"connectivity_check": "https://internettest.com"` instead of an object. |
| `WAAPI_ERROR_CONFIG_INVALID_GLOBAL_URLS_TYPE` | -91 | `connectivity_check.global_urls` exists but is **not an array of strings** | `"global_urls": "https://internettest.com"` instead of `["https://internettest.com"]`. |

When you see these errors:

- Ensure `connectivity_check` is an **object**.
- Ensure `global_urls` is an **array of strings**, not a single string.

## [**Benefits and limitations**](/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup#benefits-and-limitations)

### [Benefits](/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup#benefits)

- **Customer control over endpoints** Choose exactly which URLs or IPs are used for connectivity checks (internet or intranet).
- **Compliance with security policies**

  - Avoids unwanted calls to public sites like `google.com`.
  - Helps align with organizational, network, and regulatory restrictions.
- **Predictable network behavior**

  - All connectivity checks use a clearly defined, customer‑controlled list.
  - Easier for network and security teams to review, monitor, and approve.
- **Backward compatibility** If `connectivity_check.global_urls` is not configured, behavior remains the same as today (default `http://www.google.com`).
- **Future flexibility** The `connectivity_check` object can be extended in future releases without changing existing configurations.

### [Limitations](/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup#limitations)

- **Responsibility for endpoint availability**

  - Customers are responsible for ensuring the endpoints in `global_urls` are reachable and correctly configured.
  - If all configured endpoints are blocked or unavailable, OESIS may report that connectivity is not available, which can affect features that depend on it.
- **Configuration coordination** Some environments may require coordination between application, infrastructure, and network/security teams to select suitable URLs or IPs.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
