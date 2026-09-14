<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/encryption -->

# Encryption

Summarize Page    Connect to Cursor Connect to VS Code Warning

If "DbBackupSchedule" option has been set to *never* during or after installation, make sure you  [created a database backup](/docs/mdmft/v3.11.4/installation/updating-metadefender-managed-file-transfer) before creating a new key.

Info

If you are using MetaDefender® MFT in High Availability setup please read [this page](/docs/mdmft/v3.11.4/high-availability/changing-encryption-key) as well.

The product uses a randomly generated cryptographic key to encrypt uploaded files and other secrets.

### [Manual encryption key generation](/docs/mdmft/v3.11.4/configuration/encryption#manual-encryption-key-generation)

To generate a new cryptographic key:

1. Go to "Settings" → "Security" → "Encryption."
2. Click the "Generate Key" button.
3. Confirm the action in the appearing window.

4. Select "Cancel" to abort. Select "Confirm" to continue.
5. The new cryptographic key will be generated, and a one-time chance to download it will be provided. Store it securely in a file.

6. If storage is dismissed by mistake, generate a new encryption key. The previous key will be automatically removed by the system.

### [Automatic encryption key rotation](/docs/mdmft/v3.11.4/configuration/encryption#automatic-encryption-key-rotation)

To enable automatic encryption key rotation:

1. Go to "Settings" → "Security" → "Encryption."
2. Toggle "Enable Encryption Key Rotation" switch element
3. Choose your preferable rotation schedule

   1. Change encryption key weekly
   2. Change encryption key monthly
4. Configure schedule details

   1. Weekly: choose one day of week + time
   2. Monthly: choose day of month (1-31) + time
5. Enter a path to store rotated keys
6. Click "Save Configuration"

Warning

Cleanup of obsolete keys can take significant time, and users may be locked out of MFT until the process completes. Plan rotations outside business hours to reduce disruption.

Info

Weekly rotation is generally the most predictable option. If monthly rotation is required, select a stable day such as the 1st or 15th and run it during a non-peak time window.

The system uses the **AES algorithm** with **CBC mode** and **PKCS7 padding** to generate cryptographic keys. Newly created keys are stored as UTF8-encoded hexadecimal characters.

Once a new encryption key is generated, it will be used for all subsequent file uploads. Files uploaded prior will remain encrypted with the old keys.

Info

Obsolete keys are automatically removed when all files encrypted with those keys are deleted. Manual process is not allowed.

### [Example](/docs/mdmft/v3.11.4/configuration/encryption#example)

1. **File1** and **File2** are encrypted with **key A**.
2. User generates **key B** => **key A** becomes obsolete.
3. User uploads **File3**.
4. File3 is encrypted with **key B**.
5. System runs a cleanup check and finds that **key A** is obsolete but is still used to encrypt files **File1** and **File2;** thus, it is not removed.
6. User generates **key C** => **key B** becomes obsolete similar to **key A**.
7. User deletes files **File1** and **File3**.
8. System runs a cleanup check and deletes **key B** (obsolete + no encrypted files). **Key A** still has one file (**File2**) encrypted with it so it is left intact. **Key C** has no files encrypted with it but it is still the active key, so it remains intact, too.
