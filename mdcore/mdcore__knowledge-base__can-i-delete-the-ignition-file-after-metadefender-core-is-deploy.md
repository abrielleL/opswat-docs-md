<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/can-i-delete-the-ignition-file-after-metadefender-core-is-deploy -->

# Can I delete the ignition file after MetaDefender Core is deployed?

**Check Your Version:** This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

## [**Answer**](/docs/mdcore/knowledge-base/can-i-delete-the-ignition-file-after-metadefender-core-is-deploy#answer)

Yes. The ignition file (`ometascan.conf`) is used only during initial deployment. Core reads it to accept the EULA (End User License Agreement), import configuration, and create first user account, among other things.

Before deleting it, please confirm that MetaDefender Core is fully initialized and that you can log in normally. If initialization has not yet completed, the file is still in use and should be left in place.

## [**File location**](/docs/mdcore/knowledge-base/can-i-delete-the-ignition-file-after-metadefender-core-is-deploy#file-location)

- **Linux:** `/etc/opswat/ometascan.conf`
- **Windows:** `C:\OPSWAT\ometascan.conf`

Because the file is never consulted again on a fully deployed system, removing it has no effect on MetaDefender Core's operation. Deleting it is also good security practice since some of the sensitive information is stored in plain text.

**Support:**

If you have questions, concerns or issues regarding **MetaDefender** **Core**, please open a [Support Case](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).
