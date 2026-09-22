<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/why-does-metadefender-kiosk-hardened-image-upgrade-via-ocm-fail- -->

# Why Does MetaDefender Kiosk Hardened Image Upgrade via OCM Fail with 'The remote hostname was not found'?

**Info:**

- This article applies to MetaDefender Kiosk for Windows versions earlier than **4.8.3**.
- The issue is resolved in MetaDefender Kiosk **4.8.3** and later.

Customers may encounter a hardened image upgrade failure when the upgrade is initiated through OPSWAT Central Management (OCM). The upgrade may fail while importing OCM enrollment information and report that the remote hostname was not found.

## [**Observed Behavior in Logs**](/docs/mdkiosk/v4.8.5/knowledge-base/why-does-metadefender-kiosk-hardened-image-upgrade-via-ocm-fail-#observed-behavior-in-logs)

During the hardened image upgrade, the Kiosk may display or log an error similar to the following:

Failed to import core central management Enrollment. Error: failed to import OCM enrollment. The remote hostname was not found. Other configurations were imported. Retrying might resolve the issue

The Kiosk support package may also include related log entries.

**OCM enrollment import failure**

[12968] [Jun 27, 04:40:35:298] NetUtils.cpp#535 http::Upload(): [ERROR]
URL[http://localhost:8008/admin/import/v2] | StatusCode[400] |
{"err":"Failed to import OCM enrollment: The remote host name was not found. Other configurations were imported"}

**Core version query failure**

[2404] [Jun 27, 21:07:42:275] NetUtils.cpp#472 http::Get(): [ERROR]
URL[https://<core-hostname>:8008/version] | CURLcode[35] |
CoreClientHandler.cpp#32 core::GetCoreVersion(): [ERROR] Unable to query Core version.

Retrying the upgrade, unenrolling the Kiosk from OCM, or re-enrolling it from OCM may not resolve the issue if the same affected hardened image package is used.

## [**Cause**](/docs/mdkiosk/v4.8.5/knowledge-base/why-does-metadefender-kiosk-hardened-image-upgrade-via-ocm-fail-#cause)

In MetaDefender Kiosk versions earlier than **4.8.3**, the hardened image upgrade workflow attempts to re-enroll MetaDefender Core to OCM before the network configuration has been restored.

As a result, the Kiosk may not be able to resolve or reach the OCM/Core hostname at the moment the enrollment import is performed. This is more likely in environments that require static network settings, custom DNS, proxy settings, or specific firewall and routing configuration.

Because Core cannot reach the required host during that step, the OCM enrollment import fails and the hardened image upgrade does not complete successfully.

**Key point:** This is a product workflow sequencing issue in affected Kiosk versions, not necessarily a customer-side DNS, firewall, or configuration problem.

## [**Resolution**](/docs/mdkiosk/v4.8.5/knowledge-base/why-does-metadefender-kiosk-hardened-image-upgrade-via-ocm-fail-#resolution)

Upgrade MetaDefender Kiosk to version **4.8.3** or later and use the corresponding hardened image upgrade package that includes the fix.

In the fixed version, the upgrade workflow restores network configuration before attempting OCM re-enrollment, allowing Core to reach the central management host successfully.

- Confirm the current Kiosk version is earlier than **4.8.3**.
- Obtain and use the MetaDefender Kiosk **4.8.3-or-later** hardened image upgrade package.
- If the corrected package is not yet available in OCM, wait for the updated package before retrying the upgrade.
- Avoid repeated retries with a pre-4.8.3 hardened image package, as the same failure is expected to occur again.

## [**Recommended Troubleshooting Steps**](/docs/mdkiosk/v4.8.5/knowledge-base/why-does-metadefender-kiosk-hardened-image-upgrade-via-ocm-fail-#recommended-troubleshooting-steps)

- **Verify the affected version**

  - Confirm whether the Kiosk is running a version earlier than **4.8.3**.
  - If the version is earlier than 4.8.3 and the failure occurs during hardened image upgrade through OCM, proceed with the fixed package instead of focusing only on network troubleshooting.
- **Review support package logs**

  - Look for the OCM enrollment import failure:

Failed to import OCM enrollment: The remote host name was not found

- Look for Core version query or hostname connectivity errors:

Unable to query Core version

- **Validate network configuration if needed**

  - If the Kiosk is already on 4.8.3 or later, confirm DNS, proxy, firewall, and routing settings.
  - Confirm the OCM/Core hostname can be resolved and reached from the Kiosk after network configuration is restored.

## [**Conclusion**](/docs/mdkiosk/v4.8.5/knowledge-base/why-does-metadefender-kiosk-hardened-image-upgrade-via-ocm-fail-#conclusion)

The hardened image upgrade failure with “The remote hostname was not found” is generally caused by the upgrade workflow attempting OCM re-enrollment before network settings are restored in affected Kiosk versions. The recommended resolution is to use MetaDefender Kiosk **4.8.3** or later with the corrected hardened image upgrade package.

**Support:** If you require further assistance, please follow the instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-) before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
