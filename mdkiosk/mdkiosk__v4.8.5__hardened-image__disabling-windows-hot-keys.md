<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/hardened-image/disabling-windows-hot-keys -->

# Disabling Windows Hot Keys

You can completely disable Windows hot keys `Ctrl+Alt+Delete` and `Windows+L` from performing any actions when pressed.

## [Disabling Ctrl+Alt+Delete](/docs/mdkiosk/v4.8.5/hardened-image/disabling-windows-hot-keys#disabling-ctrlaltdelete)

1. You must first disable `Windows secure logon`, so that you do not need to press `Ctrl+Alt+Delete` from the Windows login screen. Use one of the following procedures:

- [Windows 7](http://pcsupport.about.com/od/windows7/ht/auto-logon-windows-7.htm)
- [Windows 8](http://www.eightforums.com/tutorials/5761-secure-sign-ctrl-alt-delete-enable-disable-windows-8-a.html)
- [Windows 10](https://www.tekrevue.com/tip/skip-windows-10-login-screen/)
- [Windows 2008](http://www.expta.com/2008/04/how-to-enable-autologon-for-windows.html)

2. While signed in as an Administrator, open the command line and run the following command:

reg add "HKLM\SYSTEM\CurrentControlSet\Control\Keyboard Layout" /v "Scancode Map" /t REG_BINARY /d 0000000000000000030000004de01de04be01d0000000000 /f

3. Log out of the system and log in again. To re-enable `Ctrl+Alt+Delete`, run the following command line.

reg delete "HKLM\SYSTEM\CurrentControlSet\Control\Keyboard Layout" /v "Scancode Map" /f
## [Disabling Windows+L](/docs/mdkiosk/v4.8.5/hardened-image/disabling-windows-hot-keys#disabling-windowsl)

Run the following command line:

reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\System" /v "DisableLockWorkstation" /t REG_DWORD /d 1 /f

To re-enable `Windows+L`, run the following command line:

reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\System" /v "DisableLockWorkstation" /t REG_DWORD /d 0 /f
