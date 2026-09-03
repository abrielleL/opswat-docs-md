<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/user-guide/how-can-i-restart-the-metadefender-endpoint-service- -->

# How can I restart the MetaDefender Endpoint service?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, Linux and macOS systems.

While there is generally no need to manually restart the MetaDefender Endpoint services, OPSWAT Support may instruct you to do so in certain circumstances.

To do so, follow the relevant instructions below.

## Windows (32-bit or 64-bit)

1. Open your **Services** manager.
2. Scroll down to **OPSWAT GEARS Client**.
3. Right-click on it, then select the **Restart** option.

## macOS

1. Open a **Terminal**.
2. Type: **sudo launchctl unload -w /Library/LaunchDaemons/com.opswat.GearsCLI.plist**
3. Hit **Enter**, then provide your password as prompted.
4. Next, type: **sudo launchctl load -w /Library/LaunchDaemons/com.opswat.GearsCLI.plist**
5. Hit **Enter**, then provide your password again.

## Linux

1. Open a **Terminal**.
2. Type: **sudo service opswatclient stop**
3. Hit **Enter**, then provide your password as prompted.

![](https://uploads.developerhub.io/prod/2x2P/v3uauxwoisgj20tei0pao9eb1fybzgh9l3srq0u0so2vgbj3rwgbsrz4m2tzx3qu.png)

4. Next, type: **sudo service opswatclient start**
5. Hit **Enter**, then provide your password again.

> **Support:**
>
> If you encounter any issues while attempting to **Restart The** **MetaDefender Endpoint** **Service**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
