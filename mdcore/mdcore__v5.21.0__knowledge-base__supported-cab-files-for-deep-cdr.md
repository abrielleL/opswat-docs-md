<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/supported-cab-files-for-deep-cdr -->

# What CAB files are Supported/Non-Supported by MetaDefender’s Deep CDR?

This article applies to all MetaDefender Core V5 and V4 releases deployed on Windows or Linux systems.

Please Note:

It is important to note that, among the archive files with a **.cab** filename extension, there are actually two distinct file formats, one of which is supported by Metadefender’s Deep CDR, and one of which is not.

The differences between the two **.cab** formats are outlined below.

| Type ID | **Description** | **Support to extract** |
| --- | --- | --- |
| CAB | Microsoft Cabinet Archive | **YES** |
| InstallShieldCAB | InstallShield Cabinet Archive | **NO** |

### [1. Microsoft Cabinet, Signature: MSCF](/docs/mdcore/v5.21.0/knowledge-base/supported-cab-files-for-deep-cdr#1-microsoft-cabinet-signature-mscf)

- **Cabinet** (or **CAB**) is a Microsoft Windows archive-file format that supports lossless data compression and embedded digital certificates that are used for maintaining archive integrity.
- **Cabinet** files have **.cab** filename extensions.
- **Cabinet** files are recognized by their first 4 bytes: **MSCF**.
- *Cabinet** files were originally known as **Diamond** files.

### [2. InstallShield Cabinet, Signature: ISC](/docs/mdcore/v5.21.0/knowledge-base/supported-cab-files-for-deep-cdr#2-installshield-cabinet-signature-isc)

- **InstallShield CAB** files are also archive files, but they are used by the installer program, InstallShield for its own proprietary archiving formats. Hence, they are distinct from **Microsoft Cabinet** files.
- **InstallShield CAB** files also have .**cab** file name extensions.
- **InstallShield CAB** file headers are not the same as **Microsoft CAB** files, so they are incompatible and cannot be manipulated or edited with the programs that are made to interact with the standard **Cabinet** format - including MetaDefender Core’s Deep CDR.
- There are actually numerous other (Non-Microsoft) installers that use the **.cab** extension for their proprietary archiving formats, but **InstallShield CAB** files are the most common.
- *InstallShield CAB** files are recognized by their first 3 bytes: **ISC**.

Support:

For further guidance regarding supported and non-supported **Cabinet** files, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
