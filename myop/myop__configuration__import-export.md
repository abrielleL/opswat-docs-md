<!-- source: https://www.opswat.com/docs/myop/configuration/import-export -->

# Import/Export

Administrator can use the **Import/Export** settings tab to import or export the My OPSWAT On-premises server's data, such as for backup or recovery purposes.

### [Export](/docs/myop/configuration/import-export#export)

1. To export the server's data, click the **Import/Export** drop-down menu and click **Export**.
2. In the pop-up dialog, select the data you wish to export by ticking the corresponding checkboxes.

3. Enter an encryption password for the .zip file containing the exported data. Please note that you will need this encryption password to import this file.
4. Click **Export** to confirm your selection.
5. Refresh the page in your browser. A new entry should appear in the **Export List**.
6. Click **Download** in the new entry to download the .zip file containing the exported data.

Opening the encrypted .zip file

Because the .zip file is encrypted using the AES-256 encryption method, Windows Explorer cannot open or extract it by default.

Please use a file archiver program such as 7-Zip.

### [Import](/docs/myop/configuration/import-export#import)

1. To import data from a .zip file created in [Export](/docs/myop/configuration/import-export#export), click the **Import/Export** drop-down menu and click **Import.**
2. In the pop-up dialog, upload the .zip file and enter the encryption password for that file.

3. Click **Import.** Once the import process starts, the My OPSWAT On-premises server will be temporarily inaccessible.
4. Upon success, the data will be imported to My OPSWAT On-premises.

Data Overwrite

The server's current My OPSWAT configuration and User Management settings will be replaced with the data from the import package.

The server's current Product Configurations and Product Reports will be overwritten with the data from the import package if any exists.

Users will not be able to access the My OPSWAT On-premises console during the import process.

Import limitation - Server Address

Please note that the My OPSWAT On-premises server should have the same server address (either IP address or DNS name) as the server that the import data was originally exported from. However, because product instances may accidentally report to the server before the import process completes, the server address change should be done after the data is imported successfully.

This is due to a limitation with regenerating valid download URLs for certain data types such as Product Reports.

From version 2024.3.1-OP, the setting [Server URL](/docs/myop/configuration/secure-connection#server-url) can be used to designate an address for the My OPSWAT On-premises server to solve this issue.

Import limitation - Size Limit

There is a 10 GB size limit for the import package.
