<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/getting-started/boot-from-metadefender-drive -->

# Perform a Pre-Boot Scan

## [Boot from MetaDefender Drive](/docs/mddrive/v4.4.2a/getting-started/boot-from-metadefender-drive#boot-from-metadefender-drive)

1. While your device is turned off, insert your MetaDefender Drive into the device's USB Type-A port.
2. Turn ON your device.
3. Boot from MetaDefender Drive using one of the following methods:

- **Enter the One-Time Boot Menu:**

  - **For Windows and Linux computers:** As your computer restarts, press the boot key repeatedly to enter the boot menu. The boot key varies by manufacturer. Usually, it is either F12, F9, F10, or ESC. (please refer to the manufacturer's manual).
  - **For MacBook (2018 and before):** Hold the Option `⌥` key while your MacBook starting to enter the boot menu.
  - In the boot menu, use the arrow keys to select **OPSWAT MetaDefender Drive.**
- **Change The Boot Order:**

  - **For Windows and Linux computers:**

    - As your computer restarts, press the BIOS key repeatedly to enter the BIOS setup. The boot key varies by manufacturer. Usually, it is either F12, F9, F10, or ESC. (please refer to the manufacturer's manual).
    - Use the arrow keys to navigate to the **Boot** tab.
    - In the boot order list, use the arrow keys to highlight your Drive. Then, use the designated key (usually a function key) to move the Drive to the top of the list.
    - Press `F10` to save your changes and exit BIOS. Your computer will restart and should now boot from the USB drive (which now is OPSWAT MetaDefender Drive)
  - **For MacBooks:**

    - Hold down the Option `⌥` key as your MacBook restarts to enter the Startup Manager.
    - Use the arrow keys to select **OPSWAT MetaDefender Drive** and press `↵`.
    - Restart your MacBook and it will boot from OPSWAT MetaDefender Drive.

## [**Connect to the Internet (optional)**](/docs/mddrive/v4.4.2a/getting-started/boot-from-metadefender-drive#connect-to-the-internet-optional)

- If MetaDefender Drive can't detect an internet connection, you will be prompted to manually establish a connection. Click the **Fix Internet** button to set up a Wi-fi connection.
- If your device is deployed in an offline environment, you can skip this step by clicking the **Skip Connection** button.

## [**Upgrade Drive Software**](/docs/mddrive/v4.4.2a/getting-started/boot-from-metadefender-drive#upgrade-drive-software)

Once an Internet connection has been established, MetaDefender Drive will check if its software is up to date. It is highly recommended that you upgrade your MetaDefender Drive if prompted.

In case you are using MetaDefender Drive in an offline environment, you can click the **Skip Update** button.

Warning

Skipping the **Connect to the Internet** step also skips upgrading the Drive software to its latest version. If you operate MetaDefender Drive in an offline environment, you can perform MetaDefender Drive's software and engine updates using the [MetaDefender Drive Toolkit](https://docs.opswat.com/mddrive/advanced-usages/drive-toolkit).

## [**License Verification/ Remediation**](/docs/mddrive/v4.4.2a/getting-started/boot-from-metadefender-drive#license-verification-remediation)

MetaDefender Drive will automatically attempt to detect and verify your license. If it can't find a valid license, you will be prompted to remediate it manually:

License remediation prompt

- If you have obtained an Activation Key through OPSWAT, click **Manual Input** and enter the key in the **Activation Key** field, then click **Activate**, as shown in the image below.
- If you don't have an Activation Key, you can check your internet connectivity and click the **Check for License** button.
- If MetaDefender Drive still does not accept your Activation Key or self-discover its license, please contact [OPSWAT Support](https://www.opswat.com/support).

Entering MetaDefender Drive's Activation key

## [**End-User License Agreement**](/docs/mddrive/v4.4.2a/getting-started/boot-from-metadefender-drive#end-user-license-agreement)

If you are using the plugged device for the first time, you will be prompted to read and accept MetaDefender Drive's terms of use:

License Agreement

It is required to accept OPSWAT EULA, in order to use MetaDefender Drive.

## [**Engines**](/docs/mddrive/v4.4.2a/getting-started/boot-from-metadefender-drive#engines)

- MetaDefender Drive will automatically update the engines if an active internet connection is enabled.
- You may see the message *Required engines are initializing* right below the engines list. MetaDefender Drive requires a minimum subset of initiated engines to function. As a result, it is required to wait for the engines initialization to finish before you can start performing any scan.
- It is highly recommended that you update your engines regularly via an online connection, from [OPSWAT Central Management](https://docs.opswat.com/mddrive/configuration/settings---central-management) or using the Update Downloader tool for Offline Environment.

Engine Update Minimum Requirements

Updating engines from the MetaDefender Drive OS requires the target device to have at least 8GB of RAM and to be inserted in a USB 3.0 port.

Info

Engine definitions can't be downgraded on MetaDefender Drive. Subsequent scans after a successful update will be performed using the latest definitions, for both online and offline deployments.

Info

Engines for In-Session Scanner are also downloaded together with other engines for MetaDefender Drive. You can see them in the different tab names: "**In-Session Scan**".

## [**Disks**](/docs/mddrive/v4.4.2a/getting-started/boot-from-metadefender-drive#disks)

MetaDefender Drive will automatically detect disk partitions and their file systems on the target device. Then, it will attempt to determine if the disk is encrypted.

If the disk is encrypted by BitLocker, then MetaDefender Drive will attempt to detect the encryption key in its directory.

If MetaDefender Drive can't detect an encryption key, it will allow the user to know its most likely classification of the encryption system and provide steps to unlock that Drive based on the encryption type

- Enter the Bitlocker/FileVault/LUKS password
- Enter the Bitlocker recovery key
- If MetaDefender Drive determines the drive is unencrypted, then it will simply mount it and display it as Ready.

Finally, click **Continue** to move forward, scanning the target device.

Info

Some local disk partitions might show as **Unmounted** due to being encrypted, unformulated, or formatted with an unsupported filesystem.
