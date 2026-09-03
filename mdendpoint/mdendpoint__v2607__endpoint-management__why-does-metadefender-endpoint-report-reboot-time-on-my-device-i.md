<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/endpoint-management/why-does-metadefender-endpoint-report-reboot-time-on-my-device-i -->

# Why does MetaDefender Endpoint report reboot time on my device incorrect?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows systems.

Following device shutdown, you may find that MetaDefender Endpoint reports an incorrect **Last Reboot** time, as indicated in MetaDefender IT-OT Access Console screenshot below.

![](https://uploads.developerhub.io/prod/1yda/p4nuy8zhr4uzpsxi7hqg8kwp9e5oytxs7gr4bolkhx8vvmi3nbhqsg4odezwechv.png)

This issue is usually the result of Windows **Fast Startup** settings being enabled, thereby putting your device into a hibernation state (instead of a full shutdown) whenever you press the **Power** button or click the **Shutdown** option on the power menu.

> **Please Note:**
>
> If your device supports a hibernation state, Windows will enable **Fast Startup** by default, so you will need to manually adjust these settings in order to enforce a full shutdown when you press the **Power** button or click the **Shutdown** option on the power menu.

To enable full shutdown and cold restart on your Windows device, and to avoid any issues with incorrect **Last Reboot** reporting on MetaDefender Endpoint, please follow the instructions below to turn off **Fast Startup**.

Bear in mind that the method may vary slightly, depending on your Windows version.

1. Navigate to **Control Panel\Hardware and Sound\Power Options\System Settings**.
2. Under the **When I press the power button** setting, select the **Shutdown** option, as indicated in the screenshot below.
3. Then, uncheck the **Turn on fast startup** option, as indicated below.
4. Finally, click **Save Changes** to apply your settings.

![](https://uploads.developerhub.io/prod/2x2P/cnbbi9lihr1hb02zaprvem96sy1rw3bnnnvf71a3mi9yksgibjc0i6l56rhjue3p.png)

If you would like to enable full shutdown and cold restart while keeping the **Fast Startup** setting on, please follow the instructions below.

Bear in mind that the method may vary slightly, depending on your Windows version.

1. Instead of pressing the **Power** button or clicking the **Shutdown** option, click the **Restart** option on the power menu, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/3xji7z6jlnsz4p1f7gsv6rge9tz1601b1ko2usitkwdujhal7trfhx375qaeutza.png)

2. Alternatively, you can hold down the **Shift** key while clicking the **Shutdown** option on the power menu.

> **Support:**
>
> If you have followed the instructions above but are **Still Seeing An Incorrect Last Reboot Time Reported Via MetaDefender Endpoint**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
