<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-can-i-capture-custom-information-from-end-users- -->

# How can I capture custom information from end-users?

> **Check Your Product:**
>
> This article applies to all Persistent MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

MetaDefender IT-OT Access is able to capture custom information such as email addresses, Student IDs and telephone numbers from endpoint users.

Administrators have the option to specify the nature of the information required, and to validate it using a regular expression string. These regular expression strings can be tested and validated using online regex testers like [This One](https://regex101.com/).

## [How it works](https://docs.opswat.com/macloud-sdp/kb/how-can-i-capture-custom-information-from-end-users-#how-it-works)

MetaDefender IT-OT Access will ensure that the endpoint user inputs their information via a non-optional action prompt, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/z6f676zkke25rx3kokrbstloo3ai1pyeozy06aw4wofemawbxgsvv2ve9ethbd0o.png)

Once the user inputs their information, the system reports it to the MetaDefender IT-OT Access backend servers.

Administrators can then view the information via the **MetaDefender IT-OT Access** **Console**, by navigating to **Inventory>Devices>Relevant Device>Device Details View**, where the data will be listed under **System Information**.

Administrators also have the option to search the device inventory by inputting client information, such as an email address, into the **Search** field, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/1yda/qeburdfnc4b0cg7uhxis9kxtppxk8kgusw5l9qdovvuveqaf2yk8rf4lsft3761e.png)

Once enabled, it will take between 1 and 60 minutes before the user is prompted to input their custom information, which period is based on the frequency of Client check-ins with the MetaDefender IT-OT Access backend servers.

> **Please Note:**
>
> For new MetaDefender Endpoint installs, the first MetaDefender Endpoint check-in will only take place once the installation is complete, the MetaDefender Endpoint is running, and the Client device is properly registered to a MetaDefender IT-OT Access account.

## [How to enable custom information capture](https://docs.opswat.com/macloud-sdp/kb/how-can-i-capture-custom-information-from-end-users-#how-to-enable-custom-information-capture)

1. Log into the **MetaDefender IT-OT Access Console** and navigate to **Settings>Global>Advanced**.
2. Check the option to **Enable custom information capture**.
3. Fill out the required fields, including a regular expression string and a message that will be displayed in the prompt to your endpoint users.

![](https://uploads.developerhub.io/prod/2x2P/07ys6pd6lhsyls3dj5kgk55pw0jj0n07f92x7oc8secog9xqp9afc0bcsjucsa14.png)

4. Finally, click **Save** to apply your settings.

## [How to update your regular expression string to validate user input or the message displayed to your endpoint users](https://docs.opswat.com/macloud-sdp/kb/how-can-i-capture-custom-information-from-end-users-#how-to-update-your-regular-expression-string-to-validate-user-input-or-the-message-displayed-to-your-endpoint-users)

1. Log into the **MetaDefender IT-OT Access Console** and navigate to **Settings>Global>Advanced**.
2. Under the option to **Enable custom information capture**, update the regular expression spring or message as required.
3. Finally, click **Save** to apply your changes.

> **Please Note:**
>
> If you make changes to the regular expression, the system will prompt endpoint users to re-enter their custom information.

## [How to enforce end users to re-enter their custom information](https://docs.opswat.com/macloud-sdp/kb/how-can-i-capture-custom-information-from-end-users-#how-to-enforce-end-users-to-re-enter-their-custom-information)

1. Log into the **MetaDefender IT-OT Access Console** and navigate to **Inventory>Devices**.
2. Filter for endpoints from which you wish to recapture custom information.
3. Once located, check the selection boxes alongside the appropriate devices.
4. Click on the **Actions** drop down menu in the top right-hand corner of the page, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/ecsvt0abnrcf6lf0b3hy4izjbpvi8wctz5p8ps8b65o8titithqk5ltrwrsmm6q3.png)

5. Click on the **Re-Identify** option, then confirm your selection as prompted.

![](https://uploads.developerhub.io/prod/2x2P/fiiiqlhr3zzj3iuoi3cvjc65u3276h33hwg9ou9g31rhljlpe2wcrgsb2sbzm4i5.png)

## [How to clear all captured custom information](https://docs.opswat.com/macloud-sdp/kb/how-can-i-capture-custom-information-from-end-users-#how-to-clear-all-captured-custom-information)

1. Log into the **MetaDefender IT-OT Access Console** and navigate to **Settings>Global>Advanced**.
2. Uncheck the option to **Enable custom information capture**.
3. Click **Save**, then confirm your selection as prompted.
4. The custom information capture feature is now disabled, and all captured data will be purged.

> **Support:**
>
> For any queries, concerns or issues around the **MetaDefender IT-OT Access** **Custom Information Capture Feature**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
