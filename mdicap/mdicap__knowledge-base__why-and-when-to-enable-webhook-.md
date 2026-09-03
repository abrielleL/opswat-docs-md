<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/why-and-when-to-enable-webhook- -->

# Why and when to enable webhook?

| Applies to | MetaDefender ICAP Server version 5.x. Recommended version 5.10.0 |
| --- | --- |
| Goal | Reduce MetaDefender Core load by replacing polling-based result retrieval with webhook callbacks |
| Key outcome | Fewer incoming GET requests to MetaDefender Core, and reduced application/database strain during high traffic |

#### [Overview](/docs/mdicap/knowledge-base/why-and-when-to-enable-webhook-#overview)

In a standard MetaDefender ICAP Server deployment that uses MetaDefender Core for scanning, the ICAP Server submits content for analysis and then needs a way to retrieve the final scan result.

By default, MetaDefender ICAP Server can use a polling mechanism to repeatedly query MetaDefender Core until the scan result is available. When traffic is high and/or scan durations are long, this polling can generate a very large number of HTTP GET requests.

#### [Why enable webhook callbacks](/docs/mdicap/knowledge-base/why-and-when-to-enable-webhook-#why-enable-webhook-callbacks)

When webhook callback mode is enabled on the MetaDefender Core server profile in MetaDefender ICAP Server, MetaDefender Core proactively sends a callback to MetaDefender ICAP Server with the full analysis result and the polling method is disabled.

Reduced strain on MetaDefender Core NGINX (fewer incoming GET requests)

Polling-based result retrieval can create a “many-requests-per-scan” pattern: the longer a scan takes, the more GET requests the ICAP Server sends to check for completion. Webhook callbacks change this to a “one-callback-per-scan” pattern, which significantly lowers inbound request volume to MetaDefender Core.

Practical implication: fewer inbound HTTP requests means less connection handling work in the MetaDefender Core front end (NGINX), lower request processing overhead, and fewer spikes under heavy concurrent workloads.

Example (illustrative):

- If polling interval is 20 ms (default) and a scan takes 30 seconds, one scan can trigger ~1,500 polls.
- At 200 concurrent scans, that is ~300,000 polling GET requests over those 30 seconds (before retries).
- Webhook mode removes most of those requests and replaces them with callbacks only when results are ready.

#### [Reduced strain on MetaDefender Core services and database](/docs/mdicap/knowledge-base/why-and-when-to-enable-webhook-#reduced-strain-on-metadefender-core-services-and-database)

Each polling request forces MetaDefender Core to perform work to determine the current status and/or retrieve the scan result. In typical deployments, this results in additional application processing and repeated lookups against Core’s data stores.

By disabling polling, webhook callbacks reduce the volume of status-check traffic. This helps lower pressure on MetaDefender Core’s processing pipeline and reduces database load driven by repeated result queries.

#### [Official guidance and recommendation](/docs/mdicap/knowledge-base/why-and-when-to-enable-webhook-#official-guidance-and-recommendation)

Webhook callback mode was introduced as BETA in MetaDefender ICAP Server v4.11.0 and is no longer BETA starting from v5.10.0. From v5.10.0 it is recommended to enable webhook callbacks when connecting MetaDefender ICAP Server with MetaDefender Core, because it significantly reduces the loading constraints on MetaDefender Core compared to the default polling mechanism.

#### [When to enable webhook callbacks](/docs/mdicap/knowledge-base/why-and-when-to-enable-webhook-#when-to-enable-webhook-callbacks)

- High traffic / high concurrency: many simultaneous scans increase the polling request rate and can overload MetaDefender Core during peak periods.
- Long scan durations (large files, deep analysis, slower back-end processing): longer scans generate more polls per scan and amplify Core load.
- Observed performance symptoms on MetaDefender Core: high request rates, elevated response times, or resource saturation during ICAP traffic peaks.
- You are using MetaDefender ICAP Server v5.10.0 or newer: webhook callbacks are recommended in this version line for Core integration.

#### [How to configure webhook callbacks on MetaDefender ICAP Server](/docs/mdicap/knowledge-base/why-and-when-to-enable-webhook-#how-to-configure-webhook-callbacks-on-metadefender-icap-server)

Step 1 - Enable webhook callback in the MetaDefender Core server profile

In MetaDefender ICAP Server Web Management Console:

1. Navigate to Inventory > Server profiles.
2. Create or edit the MetaDefender Core server profile used by your security rules.
3. Enable the option “Enable Webhook callback”.
4. Save the profile (and use the TEST function if available).

Step 2 - Configure webhook_address (required for multi-NIC and common for remote Core/ICAP)

If MetaDefender Core and MetaDefender ICAP Server are on different hosts, or the ICAP Server host has multiple network interfaces, set the webhook_address so MetaDefender Core knows which IP address to call back.

Linux:

• Edit /etc/mdicapsrv/mdicapsrv.conf and set:

[global] webhook_address=<ICAP_server_IP_reachable_from_Core>

Windows:

• Set the registry value under:

HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\global\webhook_address

Use-case guidance: • Different hosts: set webhook_address to the ICAP Server IP address reachable from MetaDefender Core. • Same host (Core + ICAP): webhook_address can remain 0.0.0.0.

Step 3 - Restart the MetaDefender ICAP Server service

After changing the configuration file (Linux) or registry (Windows), restart the MetaDefender ICAP Server service for changes to take effect.

Step 4 - Validate operation

- Generate a test ICAP request and confirm the request completes successfully.
- Verify that scan result retrieval no longer creates a high rate of repeated polling GET requests against MetaDefender Core.
- If you must remain on polling temporarily, you can reduce Core load by increasing the polling interval (polling_sleep) and limiting retries (polling_retry). <https://www.opswat.com/docs/mdicap/configuration/additional-tuning>

#### [Notes and best practices](/docs/mdicap/knowledge-base/why-and-when-to-enable-webhook-#notes-and-best-practices)

- Prefer MetaDefender ICAP Server v5.10.0 or newer for webhook mode, since webhook scanning is out of BETA and recommended for Core integrations in that release.
- If MetaDefender Core and MetaDefender ICAP Server are on the same host, some deployments may choose non-TLS webhook callbacks to reduce TLS negotiation overhead (where policy allows).

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
