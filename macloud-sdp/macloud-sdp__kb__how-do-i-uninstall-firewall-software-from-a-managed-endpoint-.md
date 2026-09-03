<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-do-i-uninstall-firewall-software-from-a-managed-endpoint- -->

# How do I uninstall firewall software from a managed endpoint?

This article applies to all MetaDefender IT Access products deployed on Windows, macOS and Linux systems.

MetaDefender IT Access empowers administrators to remotely uninstall Firewall software from their managed endpoint devices, via the **MetaDefender IT Access** **Console**.

To enable firewall software detection and removal from all devices linked to a policy, please follow the steps below.

1. Log into your **MetaDefender IT Access Console** and navigate to **Policy Management>Policies**.
2. Click on the policy associated with the device from which you’d like to uninstall the software, or associated with the group of devices from which you’d like to uninstall all antivirus software.
3. Inside the policy settings, expand the **Laptops/Desktops** tab, expand the **Application Control** subtab, and toggle the **Application Control** switch to its enabled state, if required, to open the application settings.
4. Click on the appropriate operating system tab to open the relevant settings.
5. Alongside **Firewall**, check all of the boxes *except* the **Disable** box. This will cause the MetaDefender Endpoint to find both installed and running firewall software, treat the issue as critical, and uninstall the software as a rule under policy.

Click **Save** to apply your settings, as illustrated in the screenshot below.

Pro Tip:

Should you follow the above steps but, in step 5, leave *both* the **Actions** settings unchecked (**Uninstall and Disable**), the system will alert you that there is a critical issue (when an unwanted app is installed or running) without automatically taking action on it.

- You will see this warning in the **Inventory>Devices>Relevant Device>Detailed Device Information>All Categories** view, where additional issue categories and/or issue warnings will appear.
- This is illustrated in the screenshot below, where a policy was set against **Antiphishing** software, and so **Antiphishing** appears as an issue warning in red.

Now, when you click on the issue warning, you will be redirected to the **Application Control** policy page, where you can choose to take further action by either uninstalling or disabling the offending software.

- This is done by checking the appropriate application control **Actions** boxes, then clicking **Save**.
Support:

If you have followed the instructions above but are having difficulty **Uninstalling Firewall Software From A Managed Endpoint Device**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
