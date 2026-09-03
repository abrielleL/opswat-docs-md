<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/why-doesn-t-metadefender-kiosk-start- -->

# Why doesn’t my MetaDefender Kiosk start?

This article applies to all MetaDefender Kiosk V4 releases deployed on Windows systems.

If your MetaDefender Kiosk fails to start, and you see the error message pictured below, it may be due to performance and slow speed issues on the machine hosting the Kiosk.

There are a variety of possible reasons for this, ranging from an underpowered CPU and low RAM, to a slow hard disk and numerous possible system errors.

To fix this issue, you will need to create a string registry key entitled **launch_delay_seconds** in the folder at path: **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\OPSWAT\MD4M** and you will need to set it to any value greater than zero.

To set this registry key, open the Windows Regedit utility before following the steps below:

- Navigate to the folder at **\HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\OPSWAT\MD4M**, as illustrated below.

- Right-click, then choose **New>String Value** from the dropdown menu, shown in the screenshot below.

- Name the new value **launch_delay_seconds**

- Double click the newly assigned String and assign it a value greater than 0 (eg. 60) seconds

- Open an elevated command prompt (as Administrator) and enter the following commands in order to restart MetaDefender Kiosk and MetaDefender Kiosk REST service:

  - net stop metadefenderSVC
  - net stop omdrest *
  - net start omdrest *
  - net start metadefenderSVC

Please Note:

*omdrest Service only applies to Metadefender Kiosk versions older and including 4.4.0.

Support:

If you have followed the instructions above but are still **Unable To Start Your** **MetaDefender Kiosk**, please follow these instructions on [How To Create a Support Package](https://docs.opswat.com/mdkiosk/troubleshooting#creating-the-package), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
