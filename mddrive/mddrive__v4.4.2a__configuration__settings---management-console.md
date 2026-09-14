<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/configuration/settings---management-console -->

# Settings → OPSWAT Management Console

Connecting with OPSWAT Central Management enables MetaDefender Drive administrators to centralize the following operations:

- Viewing and Managing scan reports
- Adjusting the settings of all MetaDefender Drive units
- Exporting reports in PDF/TXT format

Prerequisite

OPSWAT Central Management must be deployed for your organization. For more details, please find the following instructions: [OPSWAT Central Management v7](https://docs.opswat.com/ocm)

## [Connecting a MetaDefender Drive With OPSWAT Central Management](https://www.opswat.com/docs/mddrive/v4.3.3/configuration/settings---management-console#connecting-a-metadefender-drive-with-opswat-central-management)

1. After booting the MetaDefender Drive you intend to connect with My OPSWAT Central Management, go to Settings → Central Management, and check the connection status

If you are connecting to an OPSWAT Central Management Server 7.8 or later, the following options will be available:

- **Update definitions from this OCM:** check this box to allow MetaDefender Drive to fetch engine definition updates from this server
- **Update version from this OCM:** check this box to allow MetaDefender Drive to download and install its software upgrade packages from this server

To learn more about how to prepare your OPSWAT Central Management server for connection, please follow the instructions on the following pages:

- [Settings to update core modules](https://docs.opswat.com/ocm/configuration/update-settings-core-modules)

  - *Please note that the "Pushing modules update" function in* ***Folder*** *mode is not designed for MetaDefender Drive.*
- [Setting to update client vulnerability engine](https://docs.opswat.com/ocm/configuration/update-client-oesis-vul)
- [Settings to update firmware](https://docs.opswat.com/ocm/configuration/update-firmware)

2. Click Connect, then enter your My OPSWAT Central Management URL and Registration Code, that you can obtain from your My OPSWAT Central Management account, in the dialog box

Info

If your OCM is using a self-signed certificate, please make sure it is configured properly following the steps in <https://www.opswat.com/docs/mddrive/advanced-usages/ocm-https-certificates>

3. After the connection is established, you can confirm it by checking that the status of the My OPSWAT Central Management connection changed to **Managed**

When My OPSWAT Central Management is not Accessible

If a MetaDefender Drive is configured to download updates from My OPSWAT Central Management that is not accessible on boot, it is recommended to use [MetaDefender Drive Toolkit](https://docs.opswat.com/mddrive/advanced-usages/drive-toolkit) to update the scanning engines.

For MetaDefender Drive to establish a connection with an OPSWAT Central Management server using self-signed certificates, please follow the instructions on the [Using Self-signed Certificates for OPSWAT Central Management](https://docs.opswat.com/mddrive/advanced-usages/ocm-selfsigned-certificates) page.

For more details on how to manage MetaDefender Drive from OPSWAT Central Management, please refer to the [Managing MetaDefender Drive](https://onlinehelp.opswat.com/centralmgmtv7/3.3.2.8._Managing_MetaDefender_Drive.html) page.
