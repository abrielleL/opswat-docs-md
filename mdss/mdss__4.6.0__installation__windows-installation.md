<!-- source: https://www.opswat.com/docs/mdss/4.6.0/installation/windows-installation -->

# Windows Installation

## Windows package using Command Line (.msi)

From the command line interface, it is possible to install the product by executing this PowerShell command in an **Administrator** session:

```powershell
PS>msiexec /i metadefender-storage-security.msi
```

where the possible keys and their default values are the following:

| **Key** | **Description** |
| ---- | ---- |
| /quiet or /passive | Suppress the installation wizard |
| --% INSTALLFOLDER | Customize the installation directory |
| WEB_CLIENT_PORT | 80 (Web client (UI) port) |
| API_GATEWAY_PORT | 8005 |
| LICENSING_SERVICE_PORT | 5001 |
| POSTGRESQL_PORT | 5432 |
| SMB_PORT_RANGE_START | 6002(SMB starting port. Reserves 10 ports total: 5 consecutive from this value and 5 more offset by 1000) |
| SFTP_SERVICE_PORT | 5003 |
| NFS_SERVICE_PORT | 5004 |
| PG_ADMIN_PASSWORD | PostgreSQL superuser password |
| MODULE_AMAZON_S3 | Enable Amazon S3 module (1=enabled, 0=disabled) |
| MODULE_AZURE_BLOB | Enable Azure Blob module (1=enabled, 0=disabled) |
| MODULE_AZURE_FILES | Enable Azure Files module (1=enabled, 0=disabled) |
| MODULE_GOOGLE_CLOUD | Enable Google Cloud module (1=enabled, 0=disabled) |
| MODULE_ALIBABA_CLOUD | Enable Alibaba Cloud module (1=enabled, 0=disabled) |
| MODULE_SMB | Enable SMB module (1=enabled, 0=disabled) |
| MODULE_BOX | Enable Box module (1=enabled, 0=disabled) |
| MODULE_ONEDRIVE_SHAREPOINT | Enable OneDrive / SharePoint Online module (1=enabled, 0=disabled) |
| MODULE_SFTP | Enable SFTP module (1=enabled, 0=disabled) |
| MODULE_NFS | Enable NFS module (1=enabled, 0=disabled) |
| MODULE_FTP | Enable FTP module (1=enabled, 0=disabled) |
| MODULE_OPSWAT_MFT | Enable OPSWAT MFT module (1=enabled, 0=disabled) |
| MODULE_ORACLE_SDK | Enable Oracle SDK module (1=enabled, 0=disabled) |
| MODULE_SHAREPOINT_ONPREM | Enable SharePoint On-Prem module (1=enabled, 0=disabled) |

## Step by step using Install Wizard

The Install Wizard is only for the Windows installer (.msi file).

Before you begin, please make sure to read the following pages in order to install the necessary [requirements](https://www.opswat.com/docs/mdss/getting-started/windows-deployment) for each system.

1. Navigate to MetaDefender Storage Security installer location
2. Run it with Administrator privileges.

**Important:** If a local antivirus or endpoint protection solution is active, you must configure an exclusion for the MetaDefender Storage Security installation directory before running the installer. Failure to do so may result in blocked components, incomplete installation, or unstable runtime behavior. Refer to [How to Exclude the OPSWAT Folder from Windows Defender?](https://www.opswat.com/docs/mdss/knowledge-base/how-to-exclude-opswat-folder-from-anti-virus-windows-defender-) for exclusion instructions.

2. To proceed with the installation, read the License Agreement and check **I accept the terms in the License Agreement** if you accept it.

![](https://uploads.developerhub.io/prod/k8zL/s7hh8t30v7td40ddidu4x62jvndtp58v38gwf6hw4a3jmw191cjjih9v3gs4866z.png)

3. (Optional) **Configure Installation Options**
   1. Review the installation options presented in the setup wizard.
   2. Configure the **Port Configuration** section:
      1. Web Client Port: Default is 80
      2. API Gateway Port: Default is 8005
      3. Licensing Service Port: Default is 5001
      4. PostgreSQL Port: Default is 5432
      5. SMB Port Range Start: Default is 6002. This is the starting port of a range. When set, 10 ports will be reserved: 5 consecutive ports starting from this value (e.g., 6002-6006) and another 5 consecutive ports offset by 1000 (e.g., 7002-7006).
      6. SFTP Service Port: Default is 5003
      7. NFS Service Port: Default is 5004
   3. When installing MetaDefender Storage Security, you can choose which storage connection modules to enable. Each module allows integration with different storages. Select the desired **Enabled Modules** by checking the corresponding boxes
   4. Click Next to proceed with the installation

![](https://uploads.developerhub.io/prod/k8zL/i3mgdazj0gra1dna8xzasqdtpy76oqbex5msmb1osn2xe28qp6wootv6kmi3egmf.png)

> **Info — SharePoint On-Prem Module**
>
> Enabling this module requires the installation of additional SharePoint Client Components. These will be installed automatically on the next system reboot, or immediately by running the following command from a PowerShell session with Administrator privileges, from the scripts folder, once the main installation has completed:  `.\mdss.ps1 -c refresh`

> **Info**
>
> Port configuration and additional modules can be added later by modifying the customer.env file. See: [Custom configuration](https://www.opswat.com/docs/mdss/configuration/custom-configuration)

![](https://uploads.developerhub.io/prod/k8zL/v8led19dat6zwni8xki8v8oka6zrvrul6a05itry62oxbbk9ezkpkal2n9rwx42h.png)

4. To choose another installation path click **Change** and then **Browse** to the desired location. Confirm the new location by clicking **OK**.
5. Click **Next**.
6. Click **Install**.
7. Please wait while the product is being configured.

**Note**: this operation may take more than 15 minutes to complete

![](https://uploads.developerhub.io/prod/k8zL/dyqzeicz9ing90srthgoa1bq080hrlk7xrilxk0q4lri1wlu997gmf7dq4lalnof.png)

8. Installation completed successfully.

![](https://uploads.developerhub.io/prod/k8zL/3mq2jjs1jviqzc64x3xlo30ykthtx2k5xjgkhgkyqx7qwt4yj66d1fxe3jtuavqg.png)

9. Press **Finish.**

## Next steps

Production deployments should follow the [Production Considerations](https://www.opswat.com/docs/mdss/installation/production-considerations) in order to set up a remote PostgreSQL database and enable HTTPS.

After that, please follow the setup in the newly opened browser window in order to create a local administrator and complete the installation.

Please see [the onboarding page](https://www.opswat.com/docs/mdss/operations/onboarding) for more details.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
