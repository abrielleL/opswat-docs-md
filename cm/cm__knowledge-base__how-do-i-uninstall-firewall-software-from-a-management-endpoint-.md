<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-uninstall-firewall-software-from-a-management-endpoint- -->

# How do I uninstall firewall software from a management endpoint?

My OPSWAT Central Management empowers administrators to remotely uninstall Firewall software from their managed endpoint devices, via the My OPSWAT Central Management **Console**.

To enable firewall software detection and removal from all devices linked to a policy, please follow the steps below.

1. Log into your **My OPSWAT Central Management Console** and navigate to **Policy Management>Policies**.
2. Click on the policy associated with the device from which you’d like to uninstall the software, or associated with the group of devices from which you’d like to uninstall all antivirus software.
3. Inside the policy settings, expand the **Laptops/Desktops** tab, expand the **Application Control** subtab, and toggle the **Application Control** switch to its enabled state, if required, to open the application settings.
4. Click on the appropriate operating system tab to open the relevant settings.
5. Alongside **Firewall**, check all of the boxes *except* the **Disable** box. This will cause the MetaDefender Endpoint to find both installed and running firewall software, treat the issue as critical, and uninstall the software as a rule under policy.

Click **Save** to apply your settings, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/gtj0q5burqm1pe0o1hzlkix21bu49mscslez8iuwpb15mi0ob3icyy87byh1gesv.png)

> **Pro Tip:**
>
> Should you follow the above steps but, in step 5, leave *both* the **Actions** settings unchecked (**Uninstall and Disable**), the system will alert you that there is a critical issue (when an unwanted app is installed or running) without automatically taking action on it.
>
> - You will see this warning in the **Inventory>Devices>Relevant Device>Detailed Device Information>All Categories** view, where additional issue categories and/or issue warnings will appear.
> - This is illustrated in the screenshot below, where a policy was set against **Anti-phishing** software, and so **Anti-phishing** appears as an issue warning in red.
>
> ![](https://uploads.developerhub.io/prod/97qW/hk9hnzu0elp49pu0ds8qhnzocz487vgkl853jzs8kz4buvw6jd8csxxvw784y9g3.png)
>
> Now, when you click on the issue warning, you will be redirected to the **Application Control** policy page, where you can choose to take further action by either uninstalling or disabling the offending software.
>
> - This is done by checking the appropriate application control **Actions** boxes, then clicking **Save**.

> **Support:**
>
> If you have followed the instructions above but are having difficulty **Uninstalling Firewall Software From A Managed Endpoint Device**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
