<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/advanced-usages/unlocking-bitlocker-automatically-using-opswat-tool -->

# Unlock BitLocker Automatically Using OPSWAT's Tool

To unlock the BitLocker protected disks using OPSWAT's tool, users must boot Windows and then insert the OPSWAT MetaDefender Drive.

Info

If you have any encrypted removable or fixed data disks on your target device, right-click on the encrypted disk icons with the locked yellow padlock, click **Unlock Drive**, and enter the password.

To unlock BitLocket protected disks using OPSWAT tool:

1. Make sure all of the encrypted disks have been unlocked, then go to the MetaDefender Drive partition and open the tools folder.
2. The tools folder includes three files: *unlock_bitlocker.bat* (used to unlock your BitLocker drives), *unlock* bitlocker.ps1_ (a Windows PowerShell script utilized by bitlocker.bat), and *README.txt* (instructions on how to unlock BitLocker encryption for a diagnostic scan).
3. **Right-click** on *unlock_bitlocker.bat* and select **Run as administrator**, then click **Yes** when prompted to confirm running the script as administrator.

4. In the event of the disks are not completely encrypted and the status of BitLocker is showing "Waiting for activation", the tool will ask for your confirmation. Type Y if you agree to create a new RecoveryPassword protector for the disk.

5. While the script is running, a file named *bitlocker.key* will appear in the *tools* folder, indicating that the protected disk is ready to be scanned.

6. Reboot your system from MetaDefender Drive.
