<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-do-i-solve-user-authentication-issues-on-win -->

# How do I solve User Authentication issues on MetaDefender Endpoint/MetaDefender IT Access managed Windows devices?

This article applies to the current MetaDefender IT Access Console and API, and all MetaDefender Endpoint releases deployed on Windows systems.

Users running MetaDefender Endpoint on one or more Windows devices may occasionally see MetaDefender IT Access device compliance warnings/flags related to **User Authentication**, although this depends entirely on policy configurations.

These warnings/flags are triggered by device issues and will appear under **MetaDefender IT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>User Authentication**, as illustrated below.

To remediate authentication-related device compliance issues on managed Windows devices, please follow the relevant instructions below.

## [MetaDefender IT Access Compliance Warning: User Authentication - User Password Protection Is Disabled](/docs/macloud-sdp/kb/how-do-i-solve-user-authentication-issues-on-win#metadefender-it-access-compliance-warning-user-authentication---user-password-protection-is-disabled)

### [Windows 11](/docs/macloud-sdp/kb/how-do-i-solve-user-authentication-issues-on-win#windows-11)

1. Go to the Windows **Start** menu, search for **Change your password**, then click on it to open the settings, as illustrated below.

2. Click to expand the **Password** section, then click **Change**, as illustrated below.

3. Follow the wizard to set your account **Password**.
4. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT Access**) and select **Run as administrator**.

5. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

Please Note:

This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT Access servers again.

### [Windows 10](/docs/macloud-sdp/kb/how-do-i-solve-user-authentication-issues-on-win#windows-10)

1. Go to the Windows **Start** menu, search for **Change your password**, then click on it to open the settings, as illustrated below.

2. In the **Password** section, click on the **Change** button.

3. Follow the wizard to set your account **Password**.
4. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT Access**) and select **Run as administrator**.

5. Once the app is running, right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

Please Note:

This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT Access servers again.

## [MetaDefender IT Access Compliance Warning: User Authentication - Lock Screen Timeout Is Not Set](/docs/macloud-sdp/kb/how-do-i-solve-user-authentication-issues-on-win#metadefender-it-access-compliance-warning-user-authentication---lock-screen-timeout-is-not-set)

### [Windows 10/11](/docs/macloud-sdp/kb/how-do-i-solve-user-authentication-issues-on-win#windows-1011)

1. First, ensure that your **Password** is set and established on your device, by following the process outlined above.
2. With your password set, go to **Settings>Personalization>Lock screen** and click on **Screen saver** settings.
3. On the **Screen saver** settings page, set a timeout that complies with your organization’s relevant MetaDefender IT Access **Policy** requirements, by adjusting the period in the **Wait** drop-down box.
4. Check the option to **On resume, display logon screen**.

- There are two settings on **Screen and Sleep** settings. Use the first two to set Screen timeout. Then, use the last two set when your computer Sleeps.

  - The settings in the screen section will lock your screen (turns your display off) if you are inactive for the specified period of time. On the other hand, the settings in the Sleep section put your PC to sleep if you are inactive for a specified period of time.
- It is also important to note that each of the sections has a setting for when your PC is plugged to power or running on battery power.

Pro Tip:

On some devices, users may be required to restart their machine in order to apply the new settings.

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT Access**) and select **Run as administrator**.

6. Once the app is running, right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

Please Note:

This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MMetaDefender IT Access servers again.

Support:

If you have followed the instructions above but **Continue To Experience User Authentication Issues On Your** **MetaDefender Endpoint / MetaDefender IT Access** **Managed Windows Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
