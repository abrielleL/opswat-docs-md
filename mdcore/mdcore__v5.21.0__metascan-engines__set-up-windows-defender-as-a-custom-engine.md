<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/metascan-engines/set-up-windows-defender-as-a-custom-engine -->

# Set up Windows Defender as a custom engine

In order to set up and use Windows Defender as a custom engine in MetaDefender Core, the following conditions must be met:

1. The native Windows Defender / Windows Security must exist on the Windows OS.
2. **Real-time protection** must be turned on.

In case of the **Real-time protection** feature is disabled, it can be enabled on the **Manage settings** screen.

3. The MetaDefender Core **Installation** folder must be **Allowlisted** (Excluded):

The **Add or remove exclusions** feature can add a folder as an exclusion.

4. **Passive Mode** must be enabled for Windows Defender:

   1. download the [Windows_Defender_Passive_Mode](http://di7ad0dh0h2ef.cloudfront.net/KB/Core4/windows_defender_passive_mode.zip) archive and extract it.
   2. execute the **enable_windows_defender_passive_mode.reg** to automatically add the following two keys to the registry.
   3. If you want to change Windows Defender back to active mode, execute the **disable_windows_defender_passive_mode.reg** or modify the two above registries to **00000000**.

Pro Tip:

Always check if RTP is still on after enabling passive mode! If not, try disabling passive mode!

BashCopy[HKEYLOCAL MACHINE\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection]
"DisableRoutinelyTakingAction"=dword:00000001
"ForceDefenderPassiveMode"=dword:00000001Pro Tip:

Considering that this custom engine uses the native Windows Defender available on your system, the behavior of the engine relies on your Windows Defender local settings.

So, for example, if you do not want to submit files to Microsoft servers using the cloud feature, you should turn these settings off in the Windows Defender configuration.

## [Turning off Cloud protection](/docs/mdcore/v5.21.0/metascan-engines/set-up-windows-defender-as-a-custom-engine#turning-off-cloud-protection)

In order to turn off cloud protection or automatic sample submission, turn each feature off in Windows Defender’s settings
