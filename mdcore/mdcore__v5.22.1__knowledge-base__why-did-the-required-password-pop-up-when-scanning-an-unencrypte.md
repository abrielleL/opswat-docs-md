<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-did-the-required-password-pop-up-when-scanning-an-unencrypte -->

# Why did the required password pop up when scanning an unencrypted file?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This article explains why MetaDefender Core or MetaDefender Kiosk may unexpectedly prompt for a password when scanning files that are not encrypted.

## [Issue:](/docs/mdcore/v5.22.1/knowledge-base/why-did-the-required-password-pop-up-when-scanning-an-unencrypte#issue)

During the scanning of a file of [**Rocky-8.10-x86_64-dvd1.iso**](https://dynasafeazure-my.sharepoint.com/:u:/g/personal/selena_chen_dynasafe_com_tw/EQsq-OrAVrlDrEOyOXg_cZMBIA22RpQmETNL1aWa0K7Jrg?e=7Verel)

Which is the iso file from [Download - Rocky Linux](https://rockylinux.org/download)

As the file is being scanned, a password popup appears on Kiosk screen appearing that the password is needed for this file `multitoc.asc`. in order to continue scanning the file. This is happening due to the Rocky Linux preventing some users from viewing the contents of the file. (Image below)

MD Core Results

Kiosk UI

## [Current Workaround:](/docs/mdcore/v5.22.1/knowledge-base/why-did-the-required-password-pop-up-when-scanning-an-unencrypte#current-workaround)

As `multitoc.asc` is an encrypted file included by Rocky Linux, and cannot be decrypted without a valid password, the recommended workaround is to **add the hash of this file to the Allowlist**. Doing so will instruct MetaDefender Core to **bypass scanning this specific file**, allowing the rest of the ISO to be scanned without interruption.

Warning:

Before proceeding with this step, please ensure that you are **fully confident that the file is from a trusted source** and does not pose any security risks. **This action should be taken at your discretion.**

Allow list by hash

### [Additional Information:](/docs/mdcore/v5.22.1/knowledge-base/why-did-the-required-password-pop-up-when-scanning-an-unencrypte#additional-information)

Due to content protection policies by the Rocky Linux distributor, certain files within their ISO may not be accessible for scanning or extraction. Since MetaDefender Core requires access to file contents for scanning, it cannot process encrypted files like `multitoc.asc` without a password.

Unfortunately, in this scenario, **there is no alternative method to scan the encrypted file** unless valid credentials are provided.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
