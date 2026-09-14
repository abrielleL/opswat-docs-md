<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-to-remotely-validate-metadefender-kiosk-file-uploads-to-mft- -->

# How to Remotely Validate MetaDefender Kiosk File Uploads to MFT?

#### [Overview](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-remotely-validate-metadefender-kiosk-file-uploads-to-mft-#overview)

This article addresses how to validate that a MetaDefender Kiosk is functioning correctly with respect to file scanning and uploading to MetaDefender Managed File Transfer (MFT), especially when physical access to the kiosk is not possible.

#### [Issue](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-remotely-validate-metadefender-kiosk-file-uploads-to-mft-#issue)

Some users want to ensure their remote kiosks are fully operational — not just connected to MetaDefender Core, but also correctly uploading to MFT — **without requiring physical interaction**, such as inserting a USB drive.

#### [Key Points](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-remotely-validate-metadefender-kiosk-file-uploads-to-mft-#key-points)

- The **Kiosk's self-scan feature** only validates its connection to **MetaDefender Core**.
- It **does not** confirm whether file transfers to **MetaDefender MFT** are successful.
- Currently, there is **no built-in feature** in the Kiosk to simulate USB insertions remotely.

#### [Solutions & Workarounds](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-remotely-validate-metadefender-kiosk-file-uploads-to-mft-#solutions--workarounds)

**1. Use Virtual USB Emulation (Advanced Use Case)**

If your Kiosks are configured to automatically scan files from USB devices:

- You **may** use **virtual USB solutions**, such as:
- **USB/IP**
- **Emulated mass storage devices**

⚠️ **Note**: These require **pre-installed software** or **advanced configurations** on the Kiosk, which might not be feasible or supported in all environments.

**2. Use "Retrieve Files with MFT" (Recommended)**

This is a practical and supported way to validate the full workflow remotely, including file retrieval from MFT and scanning via Core.

**Steps to Validate MFT Integration:**

1. Upload a test file to MFT:

   1. You can upload as a **Guest** or **Active Directory (AD) user**, depending on how the Kiosk is configured.
2. **From the Kiosk UI**, initiate a **file retrieval session** from MFT.
3. Monitor whether:
4. The file is **downloaded** by the Kiosk
5. The file is **processed/scanned** by MetaDefender Core

**If successful, this confirms:**

- The Kiosk can **access** MFT
- The **file transfer mechanism** is operational
- The integration with **MetaDefender Core** is intact

#### [Conclusion](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-remotely-validate-metadefender-kiosk-file-uploads-to-mft-#conclusion)

Although remote USB emulation may be possible with third-party tools, using the file retrieval feature via MFT provides a simpler and more supported method to verify Kiosk functionality remotely.
