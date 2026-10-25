<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/process/configure-secure-file-storage-with-kiosk-certificate -->

# Configure Secure Storage with KIOSK's Valid Certificate

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Add Kiosk's public key to Secure Storage](/docs/mddrive/v4.4.10/process/configure-secure-file-storage-with-kiosk-certificate#add-kiosks-public-key-to-secure-storage)

To use Secure Storage with Kiosk, follow the steps to add the valid key, on a Secure Storage that does not currently have a public key

1. Tap **Kiosk Scan Validation**

2. Tap **Add Certification** button

3. Tap **Add/Replace Certification** button again to confirm the acknowledgement

4. Then this screen displays, waiting for the key. Now, connect the device to a machine that store the Kiosk public key

5. On that computer, copy the public key to the USB storage has been mounted.

6. Don't remove the cable, wait for the key to be accepted when this screen appears

7. Your Secure File Storage now is ready to be used with the Kiosk that has the information showed in the **Current Key**

Import KIOSK Cert for Secure File Storage from Central Management

From Drive version v4.4.10 and Smart Touch v2.2.0, the Certificate can be also imported from Central Management (from v.10.7.26091 and above) if MetaDefender Drive with Smart Touch has been enrolled.

## [Delete Added Cert](/docs/mddrive/v4.4.10/process/configure-secure-file-storage-with-kiosk-certificate#delete-added-cert)

1. From **Kiosk Scan Validation** screen, tap the **Delete Key**
2. To confirm deletion, tap **Yes, Delete** on the **Delete Kiosk Public Key** popup

3. Now the public key has been deleted. Repeat step **Add Kiosk's public key to Secure Storage** to add new key if you want to use the Secure File Storage with manifest feature

After configuring with valid KIOSK certificate, follow next instruction [Copy Files to Secure Files Storage](/docs/mddrive/v4.4.10/process/copy-files-to-secure-files-storage) to start using Secure File Storage.
