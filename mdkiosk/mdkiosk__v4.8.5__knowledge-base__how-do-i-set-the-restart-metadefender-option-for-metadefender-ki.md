<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-set-the-restart-metadefender-option-for-metadefender-ki -->

# How do I set the Restart MetaDefender option for MetaDefender Kiosk Watchdog on Windows 8 and above?

The following information is for users who would like to set the MetaDefender Kiosk Watchdog to the "Restart MetaDefender" option when running on Windows 8 or above.

In order for the Watchdog to be able to restart the MetaDefender Kiosk UI automatically, you will need to fully disable User Account Control (UAC) in the Windows OS. This is because in Windows 8 and above Microsoft has made the process of launching an interactive process from a service extremely difficult due to the security holes this could potentially open up. The most effective way to disable UAC is to make a change to a registry value:

1. Click **Start** and type regedit.msc to open the Registry Editor.
2. Open the registry key at HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System then find the EnableLUA registry value.
3. Set EnableLUA to 0.
4. Restart Windows.

Alternatively, you can adjust your Local Group Policy settings to disable UAC. You can only access the Group Policy Editor if you have the Professional, Enterprise, or Ultimate edition of the Windows OS.

1. Click **Start** and type "gpedit.msc" to open the Group Policy Editor.
2. Navigate to **Computer Configuration > Windows Settings > Security Settings > Local Policies > Security Options**.
3. After clicking Security Options, the right panel populates with your policies. Locate the ones for User Account Control.
4. Set **Run all administrators in Admin Approval Mode** to "Only elevate executables that are signed and validated."
5. Set **Switch to the secure desktop when prompting for elevation** to "Disabled"
6. Restart Windows.

**Note:**

Info

The steps described above will completely disable UAC on this machine. Please check with your system administrators before disabling this important Windows security feature.

Related articles :

<http://winaero.com/blog/how-to-turn-off-and-disable-uac-in-windows-10/>

<http://www.computerperformance.co.uk/win8/windows8-uac-disable.htm>
