<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-do-i-see-a-blank-white-screen-after-restarting-the-kiosk-ui- -->

# Why do I see a blank white screen after restarting the Kiosk UI?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
#### [**Issue:**](/docs/mdkiosk/v4.8.6/knowledge-base/why-do-i-see-a-blank-white-screen-after-restarting-the-kiosk-ui-#issue)

After restarting the Kiosk UI, some users may encounter a blank white screen that cannot be closed or exited.

#### [**Cause:**](/docs/mdkiosk/v4.8.6/knowledge-base/why-do-i-see-a-blank-white-screen-after-restarting-the-kiosk-ui-#cause)

This issue is commonly associated with the Kiosk application running on an unsupported, unstable, or corrupted .NET runtime. In affected environments, .NET corruption can prevent the Kiosk UI from loading properly.

#### [**Resolution:**](/docs/mdkiosk/v4.8.6/knowledge-base/why-do-i-see-a-blank-white-screen-after-restarting-the-kiosk-ui-#resolution)

Please ensure that your system is running .NET version 8 or later. If .NET 8 is already installed, upgrading to .NET version 9 is recommended to resolve potential .NET runtime corruption issues.

**Step 1**. Verify the version of .NET

1. Open a terminal/command prompt.
2. Run the following command to check your current version:

   1. **dotnet --list-runtimes**
3. Look for entries starting with Microsoft.NETCore.App and confirm the version is 8.x.x. (or later)

   1. If .NET 8 is not listed, download and install .NET from the official Microsoft website. It is recommended to install .NET version 9 if available.
4. Restart the system and then relaunch the Kiosk UI.

**Step 2.** If .NET 8.0 is already installed but the blank white screen issue continues to occur, upgrade the runtime to .NET version 9 from the official Microsoft website. This upgrade addresses known .NET corruption issues observed in affected environments.

.NET Runtime version 9 is recommended

The support for .NET 8.0 is scheduled to end in November 2026, It is recommended to upgrade to .NET 9.0 when possible.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
