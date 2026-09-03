<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/why-does-metadefender-storage-security-get-stuck-in-a-remediatio -->

# Why does MetaDefender Storage Security get stuck in a remediation loop, causing inaccessibility?

This article applies to all MetaDefender Storage Security releases deployed on Windows and Linux systems.

### [Scenario:](/docs/mdss/knowledge-base/why-does-metadefender-storage-security-get-stuck-in-a-remediatio#scenario)

In certain environments, MetaDefender Storage Security (MDSS) repeatedly retries remediation actions on specific files, even when the remediation fails or when files are already processed as *allowed* (depending on customer configuration).

As a result, multiple files may become stuck in the remediation process, eventually causing the MDSS web interface to become unresponsive until the MDSS service is restarted.

### [Root Cause](/docs/mdss/knowledge-base/why-does-metadefender-storage-security-get-stuck-in-a-remediatio#root-cause)

The remediation loop occurs when MDSS retries remediation actions multiple times without an effective retry limit per real-time process or global configuration.

By default, MDSS performs up to **3 remediation retries** with **30-second intervals**. When too many real-time processes (RTPs) are running on a single MDSS instance, **resource contention** can further increase the likelihood of remediation loops or degraded responsiveness.

### [Resolution](/docs/mdss/knowledge-base/why-does-metadefender-storage-security-get-stuck-in-a-remediatio#resolution)

- **Distribute workload** Deploy MDSS in an **active-active** model by distributing RTP workloads across multiple MDSS instances. For example: one instance handling 3 RTPs and another handling 4 RTPs instead of running all RTPs on a single instance.
- **Review remediation retry configuration** Adjust the remediation process retry parameters according to the official documentation: <https://www.opswat.com/docs/mdss/configuration/remediation-process-retries>
- **Investigate failed remediations** Check the scan report details of failed files to identify the underlying causes, such as:

  - Permission or ownership issues
  - File locking by other applications
  - Interference from antivirus or endpoint protection

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
