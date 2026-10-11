<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/how-to-update-the-bios-on-k1001-using-the-dell-optiplex-all-in-o -->

# How to Update the BIOS on K1001 using the Dell OptiPlex All-in-One Plus 7420?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article is applied to MetaDefender Core releases deployed on Linux systems in a Kubernetes container environment.

**Summary**

This article explains how to safely update the BIOS firmware on a Dell OptiPlex Plus 7420 All-in-One system to version 1.15.0, released by Dell to improve system stability, compatibility, and security.

Prerequisites

• Ensure the system is plugged into AC power (do not use battery power only).

• Backup important data in case of unexpected reboot or failure.

• Close all running applications before proceeding.

• Current BIOS version must be earlier than 1.15.0.

**Step 1: Download BIOS Update**

1. Enter Download the BIOS update 1.15.0 from the link <https://dl.dell.com/FOLDER12901410M/1/OptiPlex_7420_1.15.0.exe>

**Step 2: Install the BIOS Update**

1. Right-click the downloaded file and choose Run as Administrator.
2. If prompted by UAC, click Yes.
3. The Dell BIOS Flash Utility will open:

   - Confirm that the current version is older than 1.15.0.
   - Review warnings and click Update BIOS.
4. The system will restart automatically and enter BIOS flash mode.
5. Do not power off or interrupt the process. The system will reboot again once the update is complete.

**Step 3: Post-Update Verification**

1. After reboot, enter BIOS by pressing F2 at the Dell logo screen.
2. Check the BIOS Version in the main summary screen.

   - It should now display: 1.15.0
3. Press Esc > Save & Exit if no changes are needed.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
