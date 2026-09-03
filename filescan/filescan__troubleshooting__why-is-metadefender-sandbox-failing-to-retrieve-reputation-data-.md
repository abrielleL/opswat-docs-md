<!-- source: https://www.opswat.com/docs/filescan/troubleshooting/why-is-metadefender-sandbox-failing-to-retrieve-reputation-data- -->

# Why is MetaDefender Aether failing to retrieve reputation data due to SSL handshake errors?

This article is applied to MetaDefender Aether releases deployed on Linux systems.

### [Overview:](/docs/filescan/troubleshooting/why-is-metadefender-sandbox-failing-to-retrieve-reputation-data-#overview)

This article addresses SSL handshake errors encountered by MetaDefender Aether when attempting to retrieve reputation data from `https://api.metadefender.com` and various external sources.

### [Symptoms](/docs/filescan/troubleshooting/why-is-metadefender-sandbox-failing-to-retrieve-reputation-data-#symptoms)

- SSL handshake failures when connecting to `https://api.metadefender.com`.
- Inability to retrieve reputation data.
- Additional errors from external sources such as:

  - `alienvault.com`
  - `blocklist.de`
  - `github.com/BBcan177`
  - `darklist.de`
  - `emergingthreats.net`
  - `censys.io`

These issues often persist even after importing the main certificate and bypassing SSL inspection for `api.metadefender.com`.

### [Root Cause:](/docs/filescan/troubleshooting/why-is-metadefender-sandbox-failing-to-retrieve-reputation-data-#root-cause)

The most common cause is network-level restrictions or firewall rules that block outbound connections to required external reputation sources.

### [Resolution](/docs/filescan/troubleshooting/why-is-metadefender-sandbox-failing-to-retrieve-reputation-data-#resolution)

Follow the steps below to resolve the SSL handshake issues:

#### [1. Import the SSL Certificate](/docs/filescan/troubleshooting/why-is-metadefender-sandbox-failing-to-retrieve-reputation-data-#1-import-the-ssl-certificate)

Export the SSL certificate from `https://api.metadefender.com` in `.cer` format and install it into the trusted store:

`sudo cp _.metadefender.com.cer /usr/local/share/ca-certificates/_.metadefender.com.cer sudo update-ca-certificates`

Reboot the system to apply the changes:

`sudo reboot`

### [2. Allow External Connectivity](/docs/filescan/troubleshooting/why-is-metadefender-sandbox-failing-to-retrieve-reputation-data-#2-allow-external-connectivity)

Ensure the firewall allows outbound access to the following reputation sources:

- `alienvault.com`
- `blocklist.de`
- `github.com/BBcan177`
- `darklist.de`
- `emergingthreats.net`
- `censys.io`

### [Workarounds](/docs/filescan/troubleshooting/why-is-metadefender-sandbox-failing-to-retrieve-reputation-data-#workarounds)

If firewall adjustments are not feasible, update errors related to these external sources can be safely ignored. MetaDefender Aether uses internal reputation sources (including IP blocklists) that enable it to continue operating effectively even without external updates.

### [Additional Recommendations](/docs/filescan/troubleshooting/why-is-metadefender-sandbox-failing-to-retrieve-reputation-data-#additional-recommendations)

- Ensure the system meets minimum hardware requirements. At least **32 GB RAM** is required for stable performance. [Technical Requirements - MetaDefender Sandbox](https://www.opswat.com/docs/filescan/installation/technical-requirements)
- Regularly verify outbound network access if the environment’s security policies change.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
