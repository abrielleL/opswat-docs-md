<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/why-are-some-of-my-devices-disappearing-from-the-metaaccess-cons -->

# Why are some of my devices disappearing from the MetaDefender IT Access console?

This article applies to the current MetaDefender IT Access Console and component MetaDefender IT Access products deployed on Windows, macOS, Linux, Android and iOS systems.

MetaDefender IT Access can be configured to automatically uninstall OPSWAT Client from devices, and remove them from the device inventory (MetaDefender IT Access Console>Inventory>Devices) when they have gone unseen for a configured period.

MetaDefender IT Access can also uninstall and remove devices when they have had no access to cloud applications, or have been non-compliant for a configured number of days.

Please Note:

When a device is removed in this manner, a license token will be freed up for use on a new endpoint device.

When a device is configured to be removed from the inventory without MetaDefender Endpoint being remotely uninstalled, that device will reappear on the inventory as soon as the device reconnects to the MetaDefender IT Access server (this is known as a **Temporary Removal**). In cases where the freed device token gets spent following a temporary removal, and that token was the last available token on the account, the reappearing device will be reported as an **Out Of License Usage**.

Each of these actions (remote Client uninstall and device removal, under various conditions) are independently configurable via **MetaDefender IT Access** **Console>Settings>Global>Device Data**, as illustrated below.

As shown above, users can check the appropriate boxes, adjust the period settings, then click **Save** to apply their changes.

Support:

If you have further queries, concerns or issues regarding **Device Removal And MetaDefender Endpoint Remote Uninstall Settings**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
