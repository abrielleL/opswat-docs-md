<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/why-does-the-metadefender-kiosk-upgrade-fails-with-code-0x800706 -->

# Why does the MetaDefender Kiosk upgrade fails with code 0x80070666 when using the Windows Installer (Wizard) method?

**Check Your Version:**

This article applies when upgrading MetaDefender Kiosk from 4.7.x version to the latest version deployed on Windows systems.

## [**Overview**](/docs/mdkiosk/v4.8.5/knowledge-base/why-does-the-metadefender-kiosk-upgrade-fails-with-code-0x800706#overview)

When trying to upgrade a MetaDefender Kiosk instance from 4.7.x version to the latest version (in this case 4.7.10) the upgrade sometimes fails with error code 0x80070666. This happens because the installation of Microsoft Visual C++ redistributable v14 sometimes fails when upgrading MetaDefender Kiosk.

## [**How to fix**](/docs/mdkiosk/v4.8.5/knowledge-base/why-does-the-metadefender-kiosk-upgrade-fails-with-code-0x800706#how-to-fix)

1. Manually close the running instance of MetaDefender Kiosk.
2. Go to: [Latest Supported Visual C++ Redistributable Downloads](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)
3. Download the x86 version of the installer: <https://aka.ms/vc14/vc_redist.x86.exe>
4. Install the Visual C++ Redistributable you just downloaded.
5. Restart the computer when finished.
6. Try upgrading MetaDefender Kiosk again.

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).
