<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-relocate-installation-folder-in-metadefender-core-on-wind -->

# How to relocate installation folder in MetaDefender Core on Windows?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info:

- This article applies to all MetaDefender Core v5

**Overview**

Some users prefer to install or move the installation folder to a specific storage location but are unsure which files or folders will be created after running the installer. Creating a procedure and listing the necessary paths can help users make informed decisions when selecting or relocating installation directories.

**Use Case**

Relocating the installation folder from C:\Program Files\OPSWAT\MetaDefender Core\ to a new location, e.g., E:\OPSWAT\MetaDefender Core.

**Prerequisites**

Users need to prepare a directory in advance for storing temporary files.

**Steps to Configure**

**1. Stop the MetaDefender Core Service**

Stop the MetaDefender Core service (ometascan or OPSWAT MetaDefender Core) before proceeding.

**2. Move the Installation Folder**

Manually move the entire **MetaDefender Core** folder from: C:\Program Files\OPSWAT\MetaDefender Core to the new location: E:\OPSWAT\MetaDefender Core\

**3. Create new temp folder with full permission in the new installation folder:**

Full path of a directory to use for storing temporary files. Users need to prepare this directory in advance.

MetaDefender Core creates a subfolder called resources in this folder.

**4. Update the Windows Registry**

- Open the **Registry Editor** (regedit).
- Navigate to *Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan*
- Update the **InstallationFolder** value: Edit the **InstallationFolder** key and change its value to the new path: E:\OPSWAT\MetaDefender Core
- In *Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan\global,* add new value for tempdirectory with new data: *E:\MetaDefender Core\temp*
- Under Metascan, create a **new key** and name it **internal**.
- Inside **internal**, create a **new String value** and name it **data_directory**.
- Set the **data_directory** value to: *E:\OPSWAT\MetaDefender Core\data*
- This change ensures that MetaDefender Core correctly references the new data path for its database, updates, and other critical files.

- In *Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan\logger,* edit the new path for logfile and nginx_logfile

  1. **logfile**: E:\MetaDefender Core\data\logs\core.log
  2. **nginx_logfile**: E:\MetaDefender Core\nginx\nginx.log

- Change a Windows service executable path:

  - Navigate to *Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ometascan*
  - Change data value of Image Path to “E:\OPSWAT\MetaDefender Core\ometascan.exe”

**5.SSL configuration reset:**

MetaDefender Core relies on nginx for its web interface. On startup, nginx will check the configured location for the SSL certificate, will attempt to load it into C:\Windows\Temp\ometascan and then will start and be ready to accept connections.

If at any time the certificate is deleted or removed, nginx will no longer be able to start and this will cause Core to completely fail. the best option will be to reset the SSL configuration and, once the Core service is successfully restarted using HTTP, the certificate can be imported back into the MetaDefender Core certificate inventory and the HTTPS configuration can be reenabled.

**6. Restart MD Core service:**

Start the MetaDefender Core service (ometascan or OPSWAT MetaDefender Core) and verify that the application functions correctly in the new location.

Support:

If you require further assistance, please follow these instructions on [How to Create Support Package With Bundle Tools?](/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
