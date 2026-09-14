<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/process/smart-touch-secure-storage -->

# MetaDefender Drive with Smart Touch Operations - Secure File Storage

Secure File Storage enables using MetaDefender with Smart Touch to securely transfer files across isolated zones, by securing storing files and making them inaccessible until they are scanned by a MetaDefender Kiosk.

Media Manifest feature must be enabled in advance for MetaDefender Kiosk

For more information on how to enable and configure this feature, please follow the instructions [here](https://www.opswat.com/docs/mdkiosk/knowledge-base/how-do-i-set-up-a-media-manifest) and make sure the configurations are correct and ready to use.

If you are also using Media Validation, you can follow that all the instruction. If you are only using Secure File Storage, you just need to have Media Manifest enabled.

## [Add Kiosk's public key to Secure Storage](/docs/mddrive/v4.4.2a/process/smart-touch-secure-storage#add-kiosks-public-key-to-secure-storage)

To use Secure Storage with Kiosk, follow the steps to add the valid key, on a Secure Storage that does not currently have a public key

1. Tap **Kiosk Scan Validation**

2. Tap **Add/Replace Certification** button

3. Tap **Add/Replace Certification** button again to confirm the acknowledgement

4. Then this screen displays, waiting for the key. Now, connect the device to a machine that store the Kiosk public key

5. On that computer, copy the public key to the USB storage has been mounted.
6. Don't remove the cable, wait for the key to be accepted when this screen appears

7. Your Secure File Storage now is ready to be used with the Kiosk that has the information showed in the **Current Key**

## [Switch to Secure File Storage](/docs/mddrive/v4.4.2a/process/smart-touch-secure-storage#switch-to-secure-file-storage)

To start using Secure FIle Storage:

1. Tap the Disk Icon to expand the left navigation bar, then tap **Secure Storage**

2. Confirm your selection by tapping **Proceed to Secure Storage**

3. Secure File Storage will start first with calculating the Total Files. and the *Initializing Secure File Storage...* message will be displayed. The files count will be updated once the calculation is completed. This time of this process depends on the number of files being transferred.

4. During this initialization, if the MetaDefender Drive with Smart Touch is plugged into a computer, a small partition (with about 4.2 MB of size) containing only a busy.txt file will appear in the file browser of the target device, stating that the initialization phase is in progress.

5. Once the initialization is complete and the *Connect to a host machine to copy files* message is diplayed on the MetaDefender Drive with Smart Touch screen, Secure File Storage is ready.

## [Copy Files to Secure File Storage](/docs/mddrive/v4.4.2a/process/smart-touch-secure-storage#copy-files-to-secure-file-storage)

1. Insert MetaDefender Drive with Smart Touch with Secure File Storage enabled to the target device and wait for a new partition to appear in your file browser with the size of 32 GB and NTFS file system.

2. After the copying files is completed and the USB cable is safely unplugged, Secure File Storage will recount the files.

3. The total number of files in secure storage will be calculated after the file calculation is done.

After Copying Files into Secure File Storage

If you plug the Secure File Storage into a host you will see an empty 32GB storage that is ready for another copy session, and the files that were previously copied into Secure File Storage can only be accessed from a computer **only when they have been scanned and confirmed safe** by an OPSWAT MetaDefender Kiosk.

## [Scan Files in Secure File Storage with MetaDefender Kiosk](/docs/mddrive/v4.4.2a/process/smart-touch-secure-storage#scan-files-in-secure-file-storage-with-metadefender-kiosk)

The **Scan With MetaDefender Kiosk** button will be enabled when the file calculation is complete.

To scan file with MetaDefender Kiosk:

1. Tap **Scan With MetaDefender Kiosk**
2. Confirm that you would like to proceed with the scan when prompted

3. MetaDefender Drive with Smart Touch will start preparing files with a warning displayed to avoid cross infection because the file stored in Secure FIle Storage have not been scanned yet.

4. Once files are staged, they will be ready for scanning with Kiosk

6. Follow the steps on MetaDefender Kiosk to scan the stored files

6. During MetaDefender Kiosk processing steps, you will see 2 storage partitions.

7. Wait until the MetaDefender Kiosk scan is completed, and view the on-screen report showing how many files are Allowed or Blocked.

8. Choose to Print the scan report or not.
9. Safely unplug the USB cable once you are ready. The files will be recalculated again display the correct numbers of Clean Files, Unsafe Files, and Unscanned Files.

After a MetaDefender Kiosk Scan for Secure File Storage

On the MetaDefender Drive with Smart Touch screen, **Allowed** files will be considered as **Clean** by Secure Storage, and **Blocked** files are considered as **Unsafe Files**. Skipped files will be considered as **Unscanned Files**.

## [Securely access Clean Files in Secure File Storage](/docs/mddrive/v4.4.2a/process/smart-touch-secure-storage#securely-access-clean-files-in-secure-file-storage)

When plugging to a host computer, on its file manager, the **Clean files** **will be made visible** in a 32GB storage partition, and the **Unscanned and Unsafe files will be hidden.**

Differences in total files number between Secure File Storage and MetaDefender Kiosk or File Browser

Please notice that Secure File Storage will automatically and safely create these folder and files in the Clean storage so that Files Browser and MetaDefender Kiosk can find and scan them, but Secure File Storage will ignore them during its calcualtion.

- .OPSWAT (manifest files, session, tokens)

The following folder and files will be automatically generated by Windows operating system and will be counted by Kiosk and Secure File Storage:

- System Info folders
