<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/can-local-avs-interrupt-ongoing-scans- -->

# Can local AVs interrupt ongoing scans?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

Yes, local AV’s may interrupt ongoing scans.

Since MetaDefender Core does not include a real-time AV protection engine, many users may opt to run one or more additional real-time AV agents alongside MetaDefender Core.

Often, these anti-malware agents may already be installed on the system before the MetaDefender Core is deployed.

Please Note:

If you already have an anti-malware product installed on your system which also happens to be one of the anti-malware engines in your version of MetaDefender Core, it will interfere with the MetaDefender Core scanning process.

Similarly, these additional anti-malware agents may be responsible for blocking your MetaDefender Core files.

Pro Tip:

For this reason, OPSWAT recommends that you disable the real-time protection of your anti-malware product/s. If your corporate policy does not allow you to disable your real-time anti-virus product, you will need to add some exception rules.

**To implement your exception rule, you must exclude the following from the relevant anti-malware product’s real-time protection:**

- Exclude full installation path of MetaDefender Core.
- Exclude the temporary upload path used by MetaDefender Core.
- Exclude specific processes:

  - On Windows: “engineprocess.exe”, “engineprocess32.exe”, “ometascan.exe”, “postgres.exe” and “nginx.exe” processes.
  - On Linux: “engineprocess”, “ometascan”, “postgres” and “nginx” processes.

**If you do not add this exception or if you do not disable real-time protection, MetaDefender Core files may be blocked, results returned by MetaDefender Core scanning will not be consistent, and the return value of the scans would be one of the following:**

- **Clean**: If your existing anti-malware product was able to clean the threat
- **Failed** (or other errors): If your existing anti-malware product removed the file before MetaDefender Core could scan it.

Please Note:

If you are using Symantec Endpoint Protection as your local AV, please adjust the settings as instructed in [How do I prevent Symantec Endpoint Protection from interfering with the optimal functioning of MetaDefender Core?](/docs/mdcore/v5.21.0/knowledge-base/how-do-i-prevent-symantec-endpoint-protection-from-interfering-w)

Pro Tip:

Should you require a real time protection agent to be installed in addition to MetaDefender Core, please ensure that it is not a product featured among the MetaDefender Core’s included scanning engines.

Support:

If you need help learning how to add an exception rule (to exclude a given folder from an AV products scan area) please tell us what product you are using and we may be able to help you - but be sure to include the product version.

To contact us, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
