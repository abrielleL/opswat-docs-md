<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/knowledge-base/how-do-i-repair-a-corrupted-metadefender-email-gateway-security- -->

# How do I repair a corrupted MetaDefender Email Gateway Security database?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Email Gateway Security V4 and V5 releases deployed on Windows Systems.

1. First, download the **mdes_ps.zip** file [here](https://kb-hosting-cs.s3.amazonaws.com/KB/EmailSec5/mdes_ps.zip).
2. Before extracting the archive, ensure that it is not blocked by Windows. [Read This](https://www.tenforums.com/tutorials/5357-unblock-file-windows-10-a.html) to learn more.
3. Extract the archive to a temporary folder such as, for example: **c:\mdes_ps**.
4. Stop the MetaDefender Email Gateway Security service by opening an elevated **Powershell** and typing **net stop** **mdemailsecurity**.
5. Copy the file **C:\Program Files\OPSWAT\MetaDefender Email Security\data\mdemailsecurity.db.sqlite** to the same location that you extracted the file in step 3, for example: **c:\mdes_ps**. This file will be used in an attempt to repair the database corruption.
6. In an elevated **Powershell** (with admin permissions), run the following script.

PowershellCopycd \mdes_ps
Import-Module c:\mdes_ps\mdes.dll
Set-mdes.Repair -File c:\mdes_ps\mdemailsecurity.db.sqlitePro Tip:

The repair process may take a few minutes to run to completion. Provided there are no errors reported in the shell, your attempt to repair the corrupted database was a success.

7. Back up the original **C:\Program Files\OPSWAT\MetaDefender Email Security\data\mdemailsecurity.db.sqlite** file to a secure, alternative location.
8. Copy the **c:\mdes_ps\mdemailsecurity.db.sqlite** file to **C:\Program Files\OPSWAT\MetaDefender Email Security\data**.
9. Restart the **MetaDefender Email Gateway Security** service by opening an elevated Powershell and typing **net start ServiceName.**
10. Verify that your emails are now processing as intended.

Support:

In the unlikely event that you have followed the instructions above but are **Unable To Repair A Corrupted MetaDefender Email Gateway Security Database** , please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
