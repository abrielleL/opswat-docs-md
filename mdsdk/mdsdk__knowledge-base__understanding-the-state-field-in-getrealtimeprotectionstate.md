<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/understanding-the-state-field-in-getrealtimeprotectionstate -->

# What does the state field in GetRealTimeProtectionState mean?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Starting with Windows SDK 4.3.6669.0, `GetRealTimeProtectionState` (method `1000`) returns a new string field, `state`, alongside the existing `enabled` boolean. The field lets a caller tell a security product whose real-time protection is switched off apart from one whose services are still starting, which matters for posture checks that run right after boot or login.

`state` is present for every product that supports method `1000`, but the `initializing` and `unknown` values are currently reported only for a limited set of products whose real-time protection check has been updated to observe service startup. This article explains the values, the consistency rules with `enabled`, the current product coverage, and how to handle each value in an integration.

## [Problem](/docs/mdsdk/knowledge-base/understanding-the-state-field-in-getrealtimeprotectionstate#problem)

Access-control and VPN posture checks often call `GetRealTimeProtectionState` immediately after the endpoint boots or the user logs in. That is exactly the window in which many antivirus agents are still starting their services. Before this change, the SDK correctly reported `"enabled": false` while the backing services were not yet running, and the value flipped to `true` a few seconds later. Because the response carried only a boolean, the caller could not distinguish a product that was truly disabled from one that was still initializing, and had to block users who would be protected moments later.

## [What is the `state` field](/docs/mdsdk/knowledge-base/understanding-the-state-field-in-getrealtimeprotectionstate#what-is-the-state-field)

`state` is a string at the same level as `enabled` in `result`. It carries exactly one of four values and is never null or empty.

| Value | Meaning | `enabled` |
| --- | --- | --- |
| `enabled` | Real-time protection is on. | `true` |
| `disabled` | Real-time protection is off, or the backing services are stopped. | `false` |
| `initializing` | The product's real-time protection components are still starting up and have not reached a steady state yet (for example, a backing Windows service in `START_PENDING`). | `false` |
| `unknown` | The SDK could not determine the current state because of a transient check failure (for example, a service-state query error). | `false` |

Example response for a product that is still starting:

json_outCopy{
"result" : {
"method" : 1000,
"code" : 0,
"enabled" : false,
"state" : "initializing",
"details" : {
"antivirus" : false,
"antispyware" : false
},
"signature" : 3050,
"timing" : 0,
"timestamp" : "1777018391"
}
}

The change is additive and backward compatible. The computation and meaning of `enabled` and of the `details` object (`antivirus`, `antispyware`) are unchanged. `state` is `enabled` if and only if `enabled` is `true`; `disabled`, `initializing`, and `unknown` always appear together with `enabled: false`. Existing integrations that read only `enabled` keep working exactly as before.

## [Which products report `initializing` and `unknown`](/docs/mdsdk/knowledge-base/understanding-the-state-field-in-getrealtimeprotectionstate#which-products-report-initializing-and-unknown)

The SDK derives `initializing` and `unknown` from the state of the product's real-time protection services. This requires product-specific detection logic, so these two values are available only for products whose `GetRealTimeProtectionState` implementation has been updated. As of the October 2026 releases, the supported products are:

| Product | Platform | Available since (Windows SDK) |
| --- | --- | --- |
| Trend Micro Apex One Security Agent (also detected as Apex One Security Agent) | Windows | 4.3.6669.0 |
| SentinelOne Sentinel Agent | Windows | 4.3.6729.0 |

For all other products, `state` mirrors the existing result: `enabled` when `enabled` is `true`, `disabled` when `enabled` is `false`. These products never report `initializing` or `unknown`, so a caller must not assume that `disabled` from one of them rules out a startup race.

The list will grow as additional products are updated. Support requests for a specific product can be raised through a support case.

## [Requirements](/docs/mdsdk/knowledge-base/understanding-the-state-field-in-getrealtimeprotectionstate#requirements)

- **Windows only.** `state` is returned on Windows. macOS and Linux responses are unchanged.
- **Engine update required.** The field is produced by the SDK engine, not by data alone. An older engine loaded with newer data does not return `state`. Update to Windows SDK 4.3.6669.0 or later, and to 4.3.6729.0 or later for SentinelOne Sentinel Agent coverage.
- **Data update.** Product coverage is delivered through regular data updates, so keep the data package current to pick up newly supported products.

## [How to use `state` in an integration](/docs/mdsdk/knowledge-base/understanding-the-state-field-in-getrealtimeprotectionstate#how-to-use-state-in-an-integration)

Treat `initializing` as a signal to wait and retry rather than to block. Each call to `GetRealTimeProtectionState` performs a fresh query, so there is no need to unload and reload the SDK between attempts. A backoff of around 10 seconds between retries works well in practice.

| `state` | Recommended action |
| --- | --- |
| `enabled` | Allow. |
| `disabled` | Treat as disabled, subject to the boot-window caveat below. |
| `initializing` | Wait and retry. Do not block yet. |
| `unknown` | Apply the integration's own policy, typically retry, then fail safe. |

Boot-window caveat

If the query lands very early in boot, before the product's services have even begun starting, the SDK still returns `disabled` because the services are genuinely stopped at that moment. The lag between boot and service start is short, but for checks that run at boot or login we recommend a brief retry before treating `disabled` as final. This applies to every product, including those in the supported list above.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
