<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-are-my-engines-not-initializing-updating-over-the-internet-o -->

# Why are my Engines not initializing/updating over the Internet or OPSWAT Central Management On-Premises

**MetaDefender Core** offers several methods for updating its engines, providing flexibility to accommodate different deployment environments and security requirements. The available update methods include:

1. **Internet Update** MetaDefender Core connects directly to the **OPSWAT Update Server** (`https://update.dl.opswat.com`) to automatically initialize and update its modules.
2. **Local Folder Update** Module packages can be placed in a designated local directory, from which MetaDefender Core automatically detects and applies updates.
3. **Manual Update** Modules can be manually uploaded via the **Inventory → Modules** section within the MetaDefender Core management interface.

When **MetaDefender Core** is integrated with **OPSWAT Central Management (CM)**, a **fourth update option** becomes available, replacing the Internet Update method:

4. **Central Management Update** Engines are downloaded and deployed directly through **OPSWAT Central Management**, allowing centralized administration and streamlined maintenance across multiple MetaDefender Core instances.

### [Why Are My Engines Not Downloading/Updating via Internet or Central Management?](/docs/mdcore/knowledge-base/why-are-my-engines-not-initializing-updating-over-the-internet-o#why-are-my-engines-not-downloadingupdating-via-internet-or-central-management)

When selecting either the **Internet** or **Central Management (CM)** update option, it is crucial to ensure that direct connectivity to the respective update source is fully established.

- For **Internet updates**, MetaDefender Core must be able to connect to: `https://update.dl.opswat.com`
- For **Central Management updates**, the **Central Management** server itself must have access to the OPSWAT update server (`https://update.dl.opswat.com`) to retrieve and distribute engine updates to connected MetaDefender Core instances.

If this connectivity is blocked or restricted — due to firewall rules, proxy configuration issues, or DNS resolution problems — the engines will fail to initialize or update, resulting in errors such as the following:

- **When connected to OCM:**

[WARNING] 2025.10.14 05:04:11.131: (common.communication) Error while downloading file, url='QUrl("http://<OCM_URL>/console/core/package/<REDACTED>&deployment=<DEPLOYMENT_ID>&key=<API_KEY>&serial=1")', http_status='400', error='ProtocolInvalidOperationError', errorDetails='Error transferring http://<OCM_URL>/console/core/package/<REDACTED>&deployment=<DEPLOYMENT_ID>&key=<API_KEY>&serial=1 - server replied: ' [msgid: 485]

- **When downloading directly from Internet:**

[INFO ] 2025.10.14 05:07:28.934: (common.update) Downloading metadescriptor, downloadlink='https://update.dl.opswat.com/metadescriptor?version=<REDACTED>' [msgid: 5758]
[WARNING] 2025.10.14 05:07:28.934: (common.communication) Error while downloading file, url='QUrl("https://update.dl.opswat.com/metadescriptor?version=<REDACTED>")', http_status='0', error='HostNotFoundError', errorDetails='Host update.dl.opswat.com not found' [msgid: 485]
[ERROR ] 2025.10.14 05:07:28.949: (common.update) Error parsing metadescriptor, message='Could not download metadescriptor' [msgid: 282]

Additional references:

[**→ What links, target-services or target host-IPs need to be allowed for Metadefender Core to function accurately?**](https://www.opswat.com/docs/mdcore/knowledge-base/what-links--target-services-or-target-host-ip-s-need-to-be-allow)

[**→ What do I do if my modules disappear from the Core UI?**](https://www.opswat.com/docs/mdcore/knowledge-base/what-do-i-do-if-my-modules-disappear-from-the-core-ui-)

[**→ What do you do if your engine fails to update?**](https://www.opswat.com/docs/mdcore/knowledge-base/what-do-you-do-if-your-engine-fails-to-update-)

### [Conclusion](/docs/mdcore/knowledge-base/why-are-my-engines-not-initializing-updating-over-the-internet-o#conclusion)

Maintaining proper network connectivity is essential for ensuring smooth and consistent engine updates in MetaDefender Core. Whether updates are performed directly from the Internet or managed centrally through OPSWAT Central Management, access to `https://update.dl.opswat.com` must be verified and unrestricted.

By confirming network reachability, validating proxy settings, and ensuring correct DNS resolution, administrators can prevent update failures, maintain optimal engine performance, and ensure MetaDefender Core remains fully up to date with the latest threat intelligence and scanning capabilities.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
