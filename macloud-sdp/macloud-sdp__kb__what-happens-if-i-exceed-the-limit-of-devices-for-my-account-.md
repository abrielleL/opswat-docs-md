<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/what-happens-if-i-exceed-the-limit-of-devices-for-my-account- -->

# What happens if I exceed the limit of devices for my account?

This article applies to the current MetaDefender IT Access Console and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

Whether you have a free MetaDefender IT Access account with the functionality to monitor and manage up to 50 devices, or whether you have a paid MetaDefender IT Access account with a 50+ device limit - when the limit is reached, you will notice a number of changes.

For devices added under the device limit, nothing will change at all. Devices added once the device limit has been reached, however, will now be flagged as **Out of License Usage**.

## [Finding devices that are 'Out of License Usage'](/docs/macloud-sdp/kb/what-happens-if-i-exceed-the-limit-of-devices-for-my-account-#finding-devices-that-are-out-of-license-usage)

Administrators can filter for these devices by doing the following.

1. Navigate to **MetaDefender IT Access Console>Inventory>Devices**.
2. Click the **Filter** button in the top, right-hand corner of the screen.
3. In the pop-up menu, find the **Device Status** category, then check the **Out of License Usage** box, as illustrated below.

4. Once checked, click the **Update** button to apply the filter to your inventory.

## [What does ‘Out of License Usage’ mean?](/docs/macloud-sdp/kb/what-happens-if-i-exceed-the-limit-of-devices-for-my-account-#what-does-out-of-license-usage-mean)

- The OPSWAT Client could not report compliance data to the MetaDefender IT Access servers.
- The end user could not open the tray icon.
- The end user could not enroll/register the device to your account.
- **Out of License Usage** devices will not communicate normally with the MetaDefender IT Access servers, so out-of-date results will be returned by the MetaDefender IT Access APIs and the local registry keys.
- Integrations depending on the above APIs or registry keys will not fail, but will be based on inaccurate device statuses.

Sales:

For other devices-limit issues, or to **Add Additional Devices To Your License**, please contact the [OPSWAT Sales](https://www.opswat.com/contact) team.

Support:

For queries, concerns or issues regarding Devices **That Are Out Of License** Usage, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
