<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/why-does-auto-upgrade-for-metadefender-kiosk-hardened-image-fail -->

# Why does auto-upgrade for MetaDefender Kiosk Hardened Image fail?

This article applies to all MetaDefender Kiosk deployment using MetaDefender Kiosk hardware with the **Kiosk Hardened Image version 25.01.0** (bundled with Kiosk Application 4.7.3) or later.

**Issue:**

The auto-upgrade of the hardened image fails on MetaDefender Kiosk hardware.

**Possible Causes:**

- **BitLocker is enabled**. The auto-upgrade feature does not currently support BitLocker encryption.
- **Version conflicts.** The currently installed MetaDefender Kiosk application and/or MetaDefender Core version is newer than the version included in the latest hardened image. When this happens, the upgrade is skipped.
- **Other reasons**. The auto-upgrade could also fail if it failed to backup/restore Core/Kiosk configurations for certain reasons. In this case, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support) and provide us with the MetaDefender Core’s support package and the MetaDefender Kiosk’s support package.

  - [How to generate MetaDefender Core’s support package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-)
  - [How to generate MetaDefender Kiosk’s support package?](https://www.opswat.com/docs/mdkiosk/troubleshooting/troubleshooting-issues#generate-support-package)

**Resolution:**

- **Disable BitLocker** on the system before attempting the upgrade.
- **Downgrade** the installed version of the MetaDefender Kiosk application and/or MetaDefender Core to a version *older* than the one bundled in the latest hardened image. Refer to the [release notes](https://www.opswat.com/docs/mdkiosk/hardened-image/release-notes-image) for the specific hardened image to identify the included component versions.
- **Wait for a newer hardened image release** that includes versions greater than or equal to your currently installed Kiosk or Core versions.

Info:

Please also check for the Kiosk image upgrade known limitations at [this link](https://www.opswat.com/docs/mdkiosk/hardened-image/kiosk-image-upgrade-known-limitations).

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
