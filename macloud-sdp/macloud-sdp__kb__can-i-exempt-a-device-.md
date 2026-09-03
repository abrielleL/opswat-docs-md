<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/can-i-exempt-a-device- -->

# Can I exempt a device from a MetaDefender IT Access Policy?

This article applies to all OPSWAT MetaDefender IT Access product releases deployed on Windows, macOS, Linux, Android and iOS systems.

Yes, you can.

Making exceptions is, unfortunately, a normal part of IT and security operations, but while it may be considered a last-resort, there should still be an elegant way of handling it. With this in mind, OPSWAT has created a straightforward policy exemption mechanism for your managed devices.

Additionally, because exempt devices can potentially create security holes in your network, we’ve made it easy to audit exemption events, find exempt devices, and reverse exemptions where necessary.

Pro Tip:

While in an exempt state, devices will respond to the registry API and REST API v2 as if they were compliant.

Despite this, all compliance issues will continue to be reported in the **MetaDefender IT Access** **Console>Inventory>Devices>Device Details** view and **API** detailed responses.

## [Exempting devices from MetaDefender IT Access policy](/docs/macloud-sdp/kb/can-i-exempt-a-device-#exempting-devices-from-metadefender-it-access-policy)

There are two options for exempting devices from a policy.

### [Option 1:](/docs/macloud-sdp/kb/can-i-exempt-a-device-#option-1)

1. Log into your **MetaDefender IT Access Console** and go to **Inventory>Devices**.
2. Check the boxes alongside the devices you would like to exempt, as illustrated in the screenshot below.

3. Then click on the **Actions** dropdown menu in the top right-hand corner of the screen, framed in red in the screenshot below.

4. From the dropdown menu, select the option to **Exempt**, as illustrated below.

5. Next, select the **Period** for which you’d like to exempt the device, then click **Exempt**.

### [Option 2:](/docs/macloud-sdp/kb/can-i-exempt-a-device-#option-2)

Here, you will use the **Device Action API** to program and manage each device’s exemption state. To learn more, [Read This](/docs/macloud-sdp/developer-guide/device-action) .

## [Reversing an exemption](/docs/macloud-sdp/kb/can-i-exempt-a-device-#reversing-an-exemption)

1. Log into your **MetaDefender IT Access Console** and navigate to **Inventory>Devices**.
2. Select the devices you would like to exempt by checking the boxes in the first column.

3. Next, expand the **Actions** dropdown menu, framed in red below.

4. Select the option to **Unexempt**.

5. Finally, confirm the unexemption, as prompted.

## [Filter exempted devices](/docs/macloud-sdp/kb/can-i-exempt-a-device-#filter-exempted-devices)

Pro Tip:

To streamline device management, diagnostics and threat response, the MetaDefender IT Access Console’s **Filter** feature allows administrators to filter the devices displayed in their inventory for a wide range of characteristics, with categories including:

- Malware detection
- Compliance issues
- Issue severity
- Device status
- Device type
- Device tag
- Installed Agent
- Agent status
- Operating system
- Vulnerability severity
- Repeated issues.

When an administrator applies a filter for, for example, **Exempted Devices**, only exempted devices will be displayed in the device inventory.

1. Log into your MetaDefender IT Access Console and navigate to **Inventory> Devices**.
2. Click on the **Filters** button in the top right-hand corner of your list, as illustrated in the screenshot below.

3. A range of filtering options will be displayed, under **Device Status**, check the **Exempted** option.

4. Finally, click **Update** to apply your filters.

## [Audit log to track exemptions](/docs/macloud-sdp/kb/can-i-exempt-a-device-#audit-log-to-track-exemptions)

MetaDefender IT Access allows multiple administrators to manage a single account, so it’s essential that administrators have a way to track each other’s actions on the system.

To facilitate this, exemption actions have been added to the event logs for each device, located at **MetaDefender IT Access** **Console> Logs>Device Events**, as illustrated in the screenshot below.

Any actions taken to exempt or unexempt a device will appear in this log, along with the name of the logged-in administrator who performed the action (redacted in gray above).

The log can also be filtered so that, for example, only **Exempt/Unexempt** events appear.

Pro Tip:

Other administrative events, such as logins, logouts and policy updates, can be viewed under **MetaDefender IT Access** **Console>Logs>Admin Events**.

Support:

If you have followed the instructions above but are having difficulty **Exempting Or Unexempting Devices From A** **MetaDefender IT Access** **Policy**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
