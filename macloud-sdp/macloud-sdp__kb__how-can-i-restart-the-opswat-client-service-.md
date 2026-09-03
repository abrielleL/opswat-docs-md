<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-can-i-restart-the-opswat-client-service- -->

# How can I restart the MetaDefender Endpoint service?

This article applies to all MetaDefender Endpoint releases deployed on Windows, Linux and macOS systems.

While there is generally no need to manually restart the MetaDefender Endpoint services, OPSWAT Support may instruct you to do so in certain circumstances.

To do so, follow the relevant instructions below.

## [Windows (32-bit or 64-bit)](/docs/macloud-sdp/kb/how-can-i-restart-the-opswat-client-service-#windows-32-bit-or-64-bit)

1. Open your **Services** manager.
2. Scroll down to **OPSWAT GEARS Client**.
3. Right-click on it, then select the **Restart** option.

## [macOS](/docs/macloud-sdp/kb/how-can-i-restart-the-opswat-client-service-#macos)

1. Open a **Terminal**.
2. Type: **sudolaunchctl load -w /Library/LaunchDaemons/com.opswat.GearsCLI.plist**
3. Hit **Enter**, then provide your password as prompted.
4. Next, type: **sudo launchctl load -w /Library/LaunchDaemons/com.opswat.GearsCLI.plist**
5. Hit **Enter**, then provide your password again.

## [Linux](/docs/macloud-sdp/kb/how-can-i-restart-the-opswat-client-service-#linux)

1. Open a **Terminal**.
2. Type: **sudo service opswatclient stop**
3. Hit **Enter**, then provide your password as prompted.

4. Next, type: **sudo service opswatclient start**
5. Hit **Enter**, then provide your password again.

Support:

If you encounter any issues while attempting to **Restart The** **MetaDefender Endpoint** **Service**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
