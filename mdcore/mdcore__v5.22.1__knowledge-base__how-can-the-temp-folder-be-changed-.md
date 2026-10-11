<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-can-the-temp-folder-be-changed- -->

# How can the Temp folder be changed?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows and Linux systems.

Useful info and best practice recommendations:

- Temporary folder is used to store temporary files processed by MetaDefender Core and its engines.
- The temporary files will be cleaned up once the processing is done.
- The use of high speed IO disk for temp folder is recommended.
- Ensure sufficient space is allocated for the temp drive.

It can be changed by configuring your MetaDefender Core settings as below:

## [Linux](/docs/mdcore/v5.22.1/knowledge-base/how-can-the-temp-folder-be-changed-#linux)

- Add *tempdirectory* parameter under `[global]` section of the configuration file for the server is located in `/etc/ometascan/ometascan.conf`

## [Windows](/docs/mdcore/v5.22.1/knowledge-base/how-can-the-temp-folder-be-changed-#windows)

- Open Regedit
- Under `HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan\global` add new string value named `tempdirectory`

- Restart MetaDefender Core service

Support

If you need help configuring TEMP folder, please [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
