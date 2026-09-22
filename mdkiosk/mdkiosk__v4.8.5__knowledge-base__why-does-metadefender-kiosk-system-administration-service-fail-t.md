<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/why-does-metadefender-kiosk-system-administration-service-fail-t -->

# Why does MetaDefender Kiosk System Administration Service fail to start?

This KB applies to new installations of MetaDefender Kiosk version 4.7.5 as well as upgrades from a previous version to 4.7.5

Starting with version 4.7.5, MetaDefender Kiosk enables administrators to configure network settings - including both Ethernet and Wi-fi - directly through the Kiosk Web Management Console (WebMC). If a machine does not have the **Wireless Networking feature** installed (Windows Server does not include it by default), the Kiosk service may fail to start. In such cases, the following error may be displayed

Info

Service 'Metadefender Kiosk System Administration Service' (MDKioskSystemAdminSVC) failed to start. Verify that you have sufficient privileges to start system services.

Additionally, the Windows System Event log may contain the following entries:

Info

A timeout was reached (30000 milliseconds) while waiting for the Metadefender Kiosk System Administration Service to connect.

Info

The Metadefender Kiosk System Administration Service failed to start due to the following error: The service did not respond to the start or control request in a timely fashion.

## [Solution](/docs/mdkiosk/v4.8.5/knowledge-base/why-does-metadefender-kiosk-system-administration-service-fail-t#solution)

To resolve this issue, install the Wireless Networking feature as follows:

- Open PowerShell with administrative privileges
- Run the following command:

`Install-WindowsFeature Wireless-Networking -Restart`

After the system restarts, proceed with the Kiosk installation or upgrade process again.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
