<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/user-guide/how-can-i-make-sure-metadefender-endpoint-is-completely-removed- -->

# How can I make sure MetaDefender Endpoint is completely removed from my endpoint?

> **Info**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows and macOS systems.

> **Pro Tip:**
>
> For detailed instructions on how to uninstall MetaDefender Endpoint, please [Read This](https://docs.opswat.com/macloud-sdp/kb/how-do-i-remove-opswat-client-from-my-device-) before returning to this page to validate your uninstall and, if required, remove any remaining Client components.

In rare cases, following uninstall, certain MetaDefender Endpoint components may remain on your system, requiring manual removal.

Such instances have been well documented by the OPSWAT team, so candidate components can be easily identified and removed via the methods listed below.

## [Windows (32-bit or 64-bit)](https://docs.opswat.com/macloud-sdp/kb/how-can-i-make-sure-opswat-client-is-completely-removed-from-my-#windows-32-bit-or-64-bit)

1. Open **Task Manager** and click on the **Details** tab**.**
2. If any of the following MetaDefender Endpoint related items appear on the list, right-click them and select the **End Process** option.

- waodwd.exe
- wabpoes.exe
- wabpmsn.exe
- Gears.exe
- GearsHelper.exe
- GearsAgentService.exe
- wa_3rd_party_host_32.exe
- GearsInstaller.exe
- GearsSdkInstaller.exe
- OPSWATClientUI.exe
- owcjls.exe

![](https://uploads.developerhub.io/prod/2x2P/cmdvpt49mivlc1wg1vjev3mdpu03wna9kdx17nny36hix4rve6a7pu9bvct031v1.png)

3. Now, click on the **Services** tab to check whether either of the following services related to MetaDefender Endpoint still appear on the list.
   - **OPSWAT GEARS Client**
   - **OPSWAT GEARS Helper**
4. If either of these OPSWAT services are still running, open a **Command Prompt** and select the **Run as Administrator** option. Then, enter the appropriate command from the options below.
   - **sc delete opswatgearshelper**
   - **sc delete waondemand**
5. Once all MetaDefender Endpoint services are stopped, go to **C:\Program Files(x86)\OPSWAT** (on 64-bit) or **Program Files** (on 32-bit) and delete any of the following MetaDefender Endpoint related folders that may remain.
   - **GEARS Client**
   - **OnDemand**
   - **GEARS Client.bak**
6. Delete the following folder: **C:\ProgramData\OPSWAT\Gears**
7. Next, open **Regedit,** then find and delete the following registry keys, but take note that the **Wow6432Node** segment is omitted from the key path on 32-bit systems**.**
   - **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\OPSWAT\Gears Client**
   - **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\OPSWAT\OnDemand**
8. Search the registry for other keys containing the word **OPSWAT**, then delete them.

> **Please Note:**
>
> Users with other OPSWAT products installed on their systems (that they do not wish to uninstall) will need to check which OPSWAT registry keys are related to their other products, and then only delete the **Client** related registry keys.
>
> If you have any doubt or queries in this regard, please follow the instructions at the end of this article to contact OPSWAT Support.

9. Finally, **Restart** your machine.

## [macOS](https://docs.opswat.com/macloud-sdp/kb/how-can-i-make-sure-opswat-client-is-completely-removed-from-my-#macos)

1. Open your Activity **Monitor** and enter each of the following into the **Search** field to check whether any of the Client services are still running.

- **MetaDefender Endpoint**
- **opswat-gears-od**
- **GearsCLI**
- **GearsHelper**

2. If any of the above processes remain, do the following:

- Open **Finder** and type **/Library/LaunchDaemons** into the search field, then check the folder for any of the following files related to the MetaDefender Endpoint.
  - **com.opswar.GearsCLI.plist**
  - **com.opswat.GearsHelper.plist**
  - **com.opswat.GearsUpdater.plist**

3. Finally, **Restart** your machine.

> **Support:**
>
> For any queries about **Ensuring That MetaDefender Endpoint Is Fully Removed From Your System, Or Identifying Other OPSWAT Registry Keys**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
