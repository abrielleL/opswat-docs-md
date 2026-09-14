<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-to-update-md-kiosk-version-and-md-core-version-without-refla -->

# How to update MD Kiosk version and MD Core version without reflashing the new image?

This article applies to all MD Kiosk Secure Image versions

**Secure Image** updates are released **quarterly**, incorporating the latest Windows updates and product enhancements. Please note that upgrading the Secure Image will **replace the entire operating system**, which will also **erase the existing MetaDefender Core database** and **MetaDefender Kiosk session history**.

As an alternative, you can manually upgrade the **MD Core** and **MD Kiosk** software to avoid re-flashing the device. However, the **MD Kiosk folder is protected by the File Integrity Monitoring (FIM)** feature. To proceed with the upgrade, you must **temporarily disable FIM** before updating the Kiosk software. Follow the steps below to apply the MD Kiosk and MD Core appliance update only:

## [1. Disable the File Integrity Monitoring (FIM) feature:](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-update-md-kiosk-version-and-md-core-version-without-refla#1-disable-the-file-integrity-monitoring-fim-feature)

- Open the browser and access the link [**https://localhost/cmc**](https://localhost/cmc)
- Log in with the username and password.
- From the console, browse the settings as below:

- Right-click on the “Lock Kiosk” and choose “Unlock and allow changes”. Then wait until you see the process finished.

## [2. Upgrade software appliances:](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-update-md-kiosk-version-and-md-core-version-without-refla#2-upgrade-software-appliances)

- Download the new MD Core and MD Kiosk installers from [https://my.opswat.com](https://my.opswat.com/)
- Execute the installers to upgrade the MD Core and MD Kiosk.
- Double-check if the MD Core and MD Kiosk are working correctly.

## [3. Enable the File Integrity Monitoring (FIM) feature:](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-update-md-kiosk-version-and-md-core-version-without-refla#3-enable-the-file-integrity-monitoring-fim-feature)

- Follow step 1 to access the FIM console.
- Right-click on the “Lock Kiosk” and choose “Lock and Digital Sign…”. Then wait until the process is done.

- Refresh the web console, and make sure the status is locked.

- Restart the Kiosk and check if there are any issues afterward.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
