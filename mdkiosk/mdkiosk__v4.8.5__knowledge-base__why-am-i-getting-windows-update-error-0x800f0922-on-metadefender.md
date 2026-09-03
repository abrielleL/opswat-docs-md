<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/why-am-i-getting-windows-update-error-0x800f0922-on-metadefender -->

# Why am I getting Windows Update Error 0x800f0922 on MetaDefender Kiosk Hardened Image?

This article applies to MetaDefender Kiosks deployed on Windows 10 Enterprise LTSC 2019 version 10.0.17763.

**Issue:**

When running Windows 10 Enterprise LTSC 2019 (version 10.0.17763) on MetaDefender Kiosk, you may encounter the Windows Update error 0x800f0922.

This error typically occurs when the WinRE recovery partition is too small and must be resized. Kiosk images released before the Hardened Image 2024 Q1 may include security hardening that prevents Windows Update from resizing the WinRE partition automatically.

Beginning with Hardened Image 25.01, Windows Update is disabled. Instead, OPSWAT now provides monthly Hardened Images that include the latest Windows Updates, as well as updates for Kiosk, Core, and BIOS.

It is recommended to upgrade to the latest Hardened Image and configure scheduled image auto-upgrade in the Kiosk Console.

**Resolution:**

If you would like to update Windows on a Kiosk Hardened Image, you can use one of the following methods:

- **Re-flash a new hardened image to the latest version.** Please refer to the [Deployment Guideline](https://www.opswat.com/docs/mdkiosk/hardened-image/guideline---deploying-kiosk-hardened-image). *Note: This will erase all current settings.*
- **Use Hardened Image Auto Upgrade.** For more details, see [Auto-Upgrade Kiosk Hardened Image](https://www.opswat.com/docs/mdkiosk/hardened-image/auto-upgrade-kiosk-hardened-image).

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
