<!-- source: https://www.opswat.com/docs/mddrive/v4.4.8/advanced-usages/unlocking-bitlocker-automatically-using-windows-recovery-key -->

# Unlock BitLocker Automatically Using Windows Recovery Key

To unlock BitLocker protected disks for MetaDefender Drive using Microsoft's built-in Recover Keys, users must boot Windows and then insert the OPSWAT MetaDefender Drive.

## [Add BitLocker Recovery Keys to MetaDefender Drive](/docs/mddrive/v4.4.8/advanced-usages/unlocking-bitlocker-automatically-using-windows-recovery-key#add-bitlocker-recovery-keys-to-metadefender-drive)

If you already have BitLocker's Recovery Key files saved on your device, copy them to the MetaDefender Drive partition under the folder *Tools/BitLocker* and reboot your device from the MetaDefender Drive.

## [Generate BitLocker Recovery Keys and Add them to MetaDefender Drive](/docs/mddrive/v4.4.8/advanced-usages/unlocking-bitlocker-automatically-using-windows-recovery-key#generate-bitlocker-recovery-keys-and-add-them-to-metadefender-drive)

If you don't have the BitLocker Recovery Keys for your encrypted disk, follow these steps:

1. Plug your MetaDefender Drive into a running Windows device.
2. Right-click on the locked disk you intend to unlock, and select **Manage BitLocker**.

3. Select **Save to a file** and save the Recovery Key to a secure folder on your device. Repeat this step for every encrypted disks on the computer.
4. Copy the Recovery Key file/s to the MetaDefender Drive partition under the *tools/bitlocker* folder.

5. Reboot your system from MetaDefender Drive.
