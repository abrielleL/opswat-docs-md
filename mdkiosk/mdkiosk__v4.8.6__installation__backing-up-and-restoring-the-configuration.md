<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/installation/backing-up-and-restoring-the-configuration -->

# Backing Up and Restoring the Configuration

View as Markdown Ask ChatGPT about this page Ask Claude about this page Import from Kiosk 4.6.0 backup

As a critical issue with login via AD authentication, Kiosk 4.6.0 was removed and unable to be upgraded in place. As the result, the import of Kiosk version 4.6.0 backup is not supported either. The Kiosk administrator is advised to configure the Kiosk from the beginning.

To backup and restore Kiosk configurations, select **Configuration**, select **Backup/Restore**.

*Backup and restore Kiosk configuration on Kiosk 4.7.2 or newer*

#### [Downloading the configuration backup](/docs/mdkiosk/v4.8.6/installation/backing-up-and-restoring-the-configuration#downloading-the-configuration-backup)

Click **Download Backup** to download an archive containing the Kiosk configurations.

#### [Restoring the configuration backup](/docs/mdkiosk/v4.8.6/installation/backing-up-and-restoring-the-configuration#restoring-the-configuration-backup)

To restore the Kiosk configurations, click on the **clip icon** to upload the configuration backup file, and click **Restore**.

On **Kiosk version 4.7.2 or newer**, Administrator can select additional system settings to restore:

- Local Windows Certificates: Restore all trusted certificates from Certificate Microsoft Management Console (MMC)
- System Hosts file: Restore the custom Hosts file at *C:\Windows\System32\drivers\etc\hosts*
- License: Restore the activated Kiosk license
- Branding and Logo Customization: Restore logo and branding files found in *C:\Program Files (x86)\OPSWAT\Metadefender Kiosk\Client\en\resources*
- Secure connection: Restore the security certificate and enable Secure Connection option
- User management: Restore configured User Directories (AD, SSO and Entra ID) and accounts
- Known Wi-Fi network: Restore the known Wi-Fi networks
- Computer host name: Restore the computer name **(only available in Kiosk 4.7.3)**
- Kiosk sound: Restore custom Kiosk sound file **(only available in Kiosk 4.7.3)**
- MD Core configurations: Restore the configurations and license of MetaDefender Core **(only available in Kiosk 4.7.3)**

Issue when importing the configuration of Core 5.14 when certificate(s) is included

When importing a Core (version 5.14) configuration that includes certificate settings into Kiosk 4.7.5 or earlier, the import will fail. As a result, the connection from Kiosk and My OPSWAT to Core may be disrupted if Core URL was changed from HTTPS to HTTP.

Info

On Kiosk version 4.7.2 or newer, Administrator can backup and restore additional system settings.
