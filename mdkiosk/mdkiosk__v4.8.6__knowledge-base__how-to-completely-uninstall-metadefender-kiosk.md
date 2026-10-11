<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/how-to-completely-uninstall-metadefender-kiosk -->

# How to completely uninstall MetaDefender Kiosk

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Kiosk V4 releases deployed on Windows system.

There is no mechanism to retrieve kiosk password if admin user forgot the login password for Kiosk

management console except for a complete uninstallation.

1. Uninstall Kiosk from control panel
2. Navigate to **C:\ProgramData\OPSWAT\Metadefender**
3. Remove **KioskBackup** and **kiosk_config.zip**

Note: The folder KioskBackup available from 4.5.5+, and this will completely remove all Kiosk configuration.

Support:

If you have followed all of the steps above but are still unable to **completely uninstall MetaDefender Kiosk**, please follow these instructions on [How To Create a Support Package](https://docs.opswat.com/mdkiosk/troubleshooting#creating-the-package), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
