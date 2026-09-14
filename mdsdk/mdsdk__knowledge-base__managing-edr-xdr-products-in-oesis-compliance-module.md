<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/managing-edr-xdr-products-in-oesis-compliance-module -->

# Managing EDR/XDR Products in OESIS Compliance Module

## [**Overview**](/docs/mdsdk/knowledge-base/managing-edr-xdr-products-in-oesis-compliance-module#overview)

### [What is EDR / XDR?](/docs/mdsdk/knowledge-base/managing-edr-xdr-products-in-oesis-compliance-module#what-is-edr--xdr)

**EDR (Endpoint Detection and Response)** is an agent‑centric security solution installed on endpoints. It collects rich telemetry (processes, files, network, registry, memory, logs), detects malicious activity, supports forensic investigation (such as process trees and timelines), and enables remote containment and remediation actions from a central console.

**XDR (Extended Detection and Response)** is an evolution of EDR. Instead of focusing only on endpoints, it centralizes telemetry and detection across multiple layers: endpoints, network, cloud, email, identity, and servers. It correlates signals across these domains, orchestrates automated responses, and provides a unified investigation workspace.

A product effectively behaves as an EDR/XDR when:

- It installs an endpoint agent that collects high‑fidelity endpoint telemetry.
- It supports on‑host detection and deep forensic investigation (process trees, memory/file artifacts).
- It allows remote containment and remediation from a central console.

If a product only stores logs or raises simple alerts, and does **not** support deep endpoint forensics and remote response actions, the SDK does **not** treat it as an EDR/XDR product.

From OESIS's perspective, EDR and XDR products are handled the same way. The SDK does **not** distinguish between endpoint‑only (EDR) and cross‑domain (XDR) capabilities. Any product that we recognize as EDR/XDR is marked with the `edrxdr` label in the `labels` field when detected.

All such products share the same detection logic, connectivity checks, and method behavior in the SDK.

### [How to recognize EDR/XDR products in the SDK](/docs/mdsdk/knowledge-base/managing-edr-xdr-products-in-oesis-compliance-module#how-to-recognize-edrxdr-products-in-the-sdk)

Customers can determine whether a product is EDR/XDR using the `DetectProduct`, `GetProductInfo`, and `DiscoverProducts` methods.

A product is considered EDR/XDR when `labels.edrxdr` is `true`. If the `edrxdr` label is **missing** or explicitly set to `false`, OESIS treats that product as a **non‑EDR/XDR** solution.

Example:

json_outCopy{
"categories": [5],
"display_name": "n/a",
"labels": {
"adware": false,
"bloatware": false,
"edrxdr": true,
"pua": false,
"toolbar": false
},
"product": {
"id": 3082,
"name": "Microsoft Defender ATP"
},
"sig_name": "Microsoft Defender ATP",
"signature": 3194,
"vendor": {
"id": 90,
"name": "Microsoft Corporation"
}
}

In this example, `“edrxdr": true` indicates that Microsoft Defender ATP is treated as an EDR/XDR product by the SDK.

## [**Special behaviors for products labeled as edrxdr**](/docs/mdsdk/knowledge-base/managing-edr-xdr-products-in-oesis-compliance-module#special-behaviors-for-products-labeled-as-edrxdr)

For products labeled as `edrxdr` (that is, `labels.edrxdr = true`), OESIS performs an additional connectivity check before executing certain methods.

### [What is the connectivity check?](/docs/mdsdk/knowledge-base/managing-edr-xdr-products-in-oesis-compliance-module#what-is-the-connectivity-check)

Before running specific methods for EDR/XDR products, OESIS performs a lightweight connectivity check.

By default, the SDK sends an HTTP `GET` request to `http://google.com`. If the request succeeds, the SDK considers the endpoint online and continues with the main method.

This connectivity check is used to:

- Verify that the endpoint has general internet access.
- Help ensure that the EDR/XDR agent can reach its backend and transmit data.

If the connectivity check fails, the SDK may return an error **before** executing the main method. This avoids expensive or misleading operations when the EDR/XDR backend is likely unreachable.

You can customize or disable this behavior by:

- Changing the connectivity targets via `config.connectivity_check.global_urls` in `wa_api_setup` (see [Configuring connectivity targets via wa_api_setup](/docs/mdsdk/knowledge-base/managing-edr-xdr-products-in-oesis-compliance-module#configuring-connectivity-targets-via-wa_api_setup)).
- Skipping the connectivity check for supported methods using the `skip_connection_check` flag (see [skip_connection_check flag](/docs/mdsdk/knowledge-base/managing-edr-xdr-products-in-oesis-compliance-module#skip_connection_check-flag)).

### [Which methods are affected?](/docs/mdsdk/knowledge-base/managing-edr-xdr-products-in-oesis-compliance-module#which-methods-are-affected)

For products labeled as `edrxdr`, OESIS applies the connectivity check to:

- `GetRealTimeProtectionState`
- `GetDefinitionState`

For these methods, the SDK may fail early if connectivity is likely unavailable.

### [How to skip or customize the connectivity check](/docs/mdsdk/knowledge-base/managing-edr-xdr-products-in-oesis-compliance-module#how-to-skip-or-customize-the-connectivity-check)

You can either bypass the check for some methods or change how the check is performed.

#### [skip_connection_check flag](/docs/mdsdk/knowledge-base/managing-edr-xdr-products-in-oesis-compliance-module#skip_connection_check-flag)

OESIS exposes a `skip_connection_check` flag that lets you disable the connectivity check for specific calls.

- When `skip_connection_check = true`, the SDK does **not** perform the HTTP `GET` connectivity probe before executing the method.
- This flag is **only honored** by:

  - `GetRealTimeProtectionState`
  - `GetDefinitionState`

Use `skip_connection_check` when:

- Your application already maintains a reliable connectivity signal (e.g., a heartbeat to your own backend) and you don't need the SDK to verify it again.
- The environment blocks or heavily restricts outbound HTTP traffic (for example, no direct internet access, strict proxy rules, or `google.com` is explicitly banned), even though the EDR/XDR backend is reachable via another path.
- You are running in an air‑gapped or intranet‑only network where external URLs like `http://google.com` are unreachable, but the EDR/XDR agent can still communicate with internal infrastructure.
- The connectivity check introduces unacceptable latency (e.g., DNS resolution timeouts in restricted environments) and you want faster method execution.
- You already have a connectivity validation layer at the application or platform level, and redundant checking by the SDK adds no value.

When you disable the check, the SDK will no longer “fail fast” on connectivity issues for these two methods. You are responsible for handling connectivity validation at a higher level if that is important for your application.

#### [Configuring connectivity targets via wa_api_setup](/docs/mdsdk/knowledge-base/managing-edr-xdr-products-in-oesis-compliance-module#configuring-connectivity-targets-via-wa_api_setup)

You can configure which targets OESIS uses for connectivity checks through `wa_api_setup`, by setting `config.connectivity_check.global_urls`. This should be a list of URLs or IPs the SDK will probe to determine reachability.

Detailed guide

For a detailed guide of how to configure URL for checking internet connectivity, please refer to the dedicated article: [Support configuring connectivity check URLs through wa_api_setup](/docs/mdsdk/knowledge-base/support-configuring-connectivity-check-urls-through-wa-api-setup)

By default, the SDK validates connectivity with an HTTP `GET` to `http://google.com`

Override the default when:

- `<http://google.com>` is blocked, intercepted, or not representative of actual EDR/XDR traffic in your environment, and
- You still want to keep the SDK’s built‑in connectivity gating behavior for the affected methods.

In this case, you configure `global_urls` to use destinations that are both reachable and meaningful for your environment (for example, your EDR/XDR vendor endpoints or internal connectivity check hosts).

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
