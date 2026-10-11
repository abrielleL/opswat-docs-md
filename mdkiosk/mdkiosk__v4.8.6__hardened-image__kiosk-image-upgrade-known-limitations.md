<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations -->

# Kiosk Image Upgrade Known Limitations

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [General limitations of upgrade feature](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#general-limitations-of-upgrade-feature)

- **Local MetaDefender Core restoration only**:

  - Only Local MetaDefender Core that is integrated with Kiosk is restored configuration after upgrade, the configurations of remote Core are not backed up or restored.
  - In the Kiosk WebMC settings under Configuration > Integration > MetaDefender Core, the value must be set to either "localhost", "127.0.0.1", or left blank.
- **Wi-Fi with Credentials not supported:** Wi-Fi configurations that requires user credentials are not supported by the backup process.
- **MD Core quarantine files backup:**

  - Kiosk only supports backing up quarantine files from MD Core. The quarantine files will not be shown from Core WebMC, downloading quarantine files must be done via REST API here.
  - Quarantined files in MetaDefender Core will only be kept after upgrade if user utilizes "Quarantine blocked files in Core" on Kiosk blocked file handling configuration.
  - Critical setting such as the Core API key and DB PIN must match the value used during this backup process. If these values differ, the restoration process may fail.
- **MD Core deployment ID changed:** Switching between Ethernet and Wi-Fi after activating MD Core may cause the Kiosk upgrade to fail and roll back due to a change in the MD Core Deployment ID.
- **BitLocker must be disabled** on the C drive: as Kiosk currently only supports upgrades when BitLocker is turned off.
- **Network Hardening Policy blocks upgrades:** If **Network Hardening Policy** (Settings > System Hardening) is turned on, the Kiosk image upgrade cannot back up the current firewall and network configuration and will fail. To upgrade a device that has this policy enabled, turn off Network Hardening Policy, complete the upgrade, and then re-enable it once the upgrade finishes. After re-enabling, confirm that network-related services return to their expected state before returning the device to service.
- **Domain-joined system settings will not be restored.**
- Only Windows administrator accounts are restored when using the preconfigured local administrator password. The standard users are not supported.
- When the backup file is too large (e.g ~10GB) due to accumulated MD Core quarantines file, the backup may hang at 95%
- **Preserved folder encryption is not retained:** If a folder configured under Preserved folders was encrypted (e.g., via Windows EFS) before the upgrade, it may no longer be encrypted after being restored.
- **No warning when preserved folders exceed the size limit:** The Kiosk Console may not currently warn if the combined size of all configured preserved folders exceeds the 10 GB limit when the setting is saved. Administrators should manually confirm their preserved folders stay within 10 GB in total.

BIOS version remains the same after the rollback

When rolling back from Kiosk Hardened Image 25.08.0 to 25.07.1 (or older versions), the BIOS version may not be downgraded, as Dell no longer supports downgrading the BIOS

## [Troubleshooting](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#troubleshooting)

If an error occurs during the upgrade process, navigate to **Upgrades > Upgrade History** and review the Application Logs to obtain detailed error messages. This section outlines common upgrade issues and provides corresponding remediation actions.

### [Operating System related issues](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#operating-system-related-issues)

#### [BitLocker is enabled](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#bitlocker-is-enabled)

| Name | Description |
| --- | --- |
| Error Details | Error message in the upgrade history: "Failed to setup ReOS: BitLocker is enabled on the 'Windows' partition" |
| Remediation | Disable BitLocker for the C volume before performing the upgrade |

#### [Insufficient Free Space](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#insufficient-free-space)

| Name | Description |
| --- | --- |
| Error Details | Error message in the upgrade history: "Insufficient free space to re - partition.The 'Windows' partition must have at least <n> GB of free space" |
| Remediation | Ensure that the C: drive has at least the amount of free space specified in the error message. |

#### [Cannot create the upgrade partition](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#cannot-create-the-upgrade-partition)

| Name | Description |
| --- | --- |
| Error Details | Error message in the upgrade history: "Failed to set up ReOS: Failed to shrink and create the upgrade partition" |
| Remediation | Go to Disk Management, delete the shrunk volume  Follow the steps from Windows documentation to address issue timeout when creating partition.   - Open an elevated Command Prompt. To do it, click Start, click All Programs, click Accessories, right-click Command Prompt, and then click Run as administrator. - Type the following command and then press Enter: `sfc /verifyonly` - Let the command operation complete:`sfc /scannow`   Retry to upgrade |

#### [System crash during upgrade](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#system-crash-during-upgrade)

| Name | Description |
| --- | --- |
| Error Details | The system may fail to upgrade and remain on the current version without any entry in the upgrade history if any of the following issues occur during the upgrade process:   - Forced shutdown or power outage - System crash (Blue Screen of Death - BSOD) |
| Remediation | For MD Core versions prior to 5.14.0, verify if the license has been deactivated. If so, reactivate the license.  Retry the upgrade process |

#### [Failed to get user profile path](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#failed-to-get-user-profile-path)

| Name | Description |
| --- | --- |
| Error Details | Error message in the upgrade history: "Failed to backup data. An unexpected result occoured. Failed to get user profile path" |
| Remediation | When the upgrade was triggered, no Windows user was logged in — the Kiosk may have been at the lock screen. Please log in with an admin user and retry the upgrade process. |

#### [Failed to setup ReOS](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#failed-to-setup-reos)

| Name | Description |
| --- | --- |
| Error Details | Error message in the upgrade history: "Failed to setup ReOS: Unable to free enough space to continue the backup process" |
| Remediation | Pagefile (pagefile.sys) detected on system drive. Pagefile cannot be automatically disabled during upgrade (requires system reboot). If shrink fails, manual intervention is required:   1. Disable pagefile:     - Open System Properties > Advanced > Performance Settings > Advanced tab    - Under Virtual Memory, click 'Change'    - Uncheck 'Automatically manage paging file size for all drives'    - Select 'No paging file' and click 'Set' 2. Reboot the system 3. Retry the upgrade 4. After successful upgrade, re-enable pagefile if desired |

#### [Upgrade fails with Network Hardening Policy enabled](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#upgrade-fails-with-network-hardening-policy-enabled)

| Name | Description |
| --- | --- |
| Error Details | The upgrade fails to back up firewall and network configuration on a device that has Network Hardening Policy enabled. |
| Remediation | Go to **Settings > System Hardening**, turn off Network Hardening Policy, and restart the device to apply the change. Retry the upgrade. Once the upgrade completes successfully, you can re-enable Network Hardening Policy. |

### [MD Core configuration related issues](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#md-core-configuration-related-issues)

#### [Failed to backup Core certificates](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#failed-to-backup-core-certificates)

| Name | Description |
| --- | --- |
| Error Details | Error message in the upgrade history: "Failed to export the Core certificates. Certificate key file is protected by a passphrase" |
| Remediation | Temporarily remove the certificates that use passphrases from the MD Core Inventory and any associated usages, especially the one is using to enable HTTPS on Core. Refer to MD Core documentation for more details. |

#### [Invalid MD Core API key is configured](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#invalid-md-core-api-key-is-configured)

| Name | Description |
| --- | --- |
| Error Details | Error message in the upgrade history: "Failed to export the Core certificates. Core certificates export failed. Access denied" |
| Remediation | Go to the Kiosk console to update the valid Core URL and API key  Navigate to the Core console to verify the license status, as the license may become inactive. |

#### [Failed to backup MD Core license](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#failed-to-backup-md-core-license)

| Name | Description |
| --- | --- |
| Error Details | Error message in the upgrade history: "Failed to backup Core's license. Core license deactivation failed. The current Core license is either offline activated or has expired" or "Failed to import Core license : There are some issues with the current license; re-activate it to resolve the problem" |
| Remediation | Double-check if the license of integrated MD Core is still valid  For versions prior 5.14.0, if it is activated offline or activated from My OPSWAT:   - Upgrade to MD Core version at least 5.14.0, or - Reactivate the MD Core with online activation |

#### [Kiosk has rollbacked after failed to import MD Core license](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#kiosk-has-rollbacked-after-failed-to-import-md-core-license)

| Name | Description |
| --- | --- |
| Error Details | Kiosk has rollbacked after failed to import MD Core license with error the upgrade history: "Failed to import license. Other configurations were imported" |
| Remediation | If the MetaDefender Core license was activated online, double-check the network connectivity and ensure the Kiosk can access the internet after the upgrade. Reactivate MD Core using the current active network to prevent the Deployment ID from changing after the upgrade, as noted in the limitations.  Retry to upgrade. |

### [Kiosk application related issues](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#kiosk-application-related-issues)

#### [The upgrade resource is invalid](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-image-upgrade-known-limitations#the-upgrade-resource-is-invalid)

|  |  |
| --- | --- |
| Error Details | Error message in the upgrade history: "The provided resources are invalid for the upgrade" As a security measure during the upgrade process, Kiosk performs an integrity check on the downloaded packages before proceeding. In this case, the packages failed the integrity check, possibly due to file corruption or a hash mismatch during the download over the internet. |
| Remediation | Delete all previously downloaded upgrade packages from the following path: `C:\ProgramData\OPSWAT\Metadefender\Upgrade\Package`  Upgrade to Kiosk version **4.7.7**. From this version onward, Kiosk will ensure to clear any invalid upgrade packages. |
