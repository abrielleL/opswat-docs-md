<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/storage-units -->

# Integrations

MetaDefender Storage Security integrates with various cloud and on-premises storage solutions, represented as **storage units**.

We provide a list (see table below) of officially supported integrations that are continuously tested for full functionality.

> **IMPORTANT
>
> Please get in touch with us if your specific storage provider isn't shown.**
>
> We likely already support storage systems that use S3-compatible interfaces or standard protocols such as SMB, NFS, or SFTP.

## Cloud Object Storages

| Storage Name | Integration Type | Tagging | Event-Based | Metadata * Copy |
| ---- | ---- | ---- | ---- | ---- |
| [Amazon S3](https://www.opswat.com/docs/mdss/integrations/add-an-amazon-s3-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-aws-example) | Yes |
| [Wasabi](https://www.opswat.com/docs/mdss/integrations/add-a-wasabi-storage) | S3 Compatible | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Cloudian®](https://www.opswat.com/docs/mdss/integrations/add-a-cloudian-storage) | S3 Compatible | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Oracle Cloud](https://www.opswat.com/docs/mdss/integrations/add-an-oracle-cloud-storage) | S3 Compatible | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Oracle Cloud](https://www.opswat.com/docs/mdss/integrations/add-an-oracle-sdk-storage) | Native | No | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-handling-for-oraclesdk) | Yes |
| [MinIO](https://www.opswat.com/docs/mdss/integrations/add-a-minio-storage) | S3 Compatible | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Cubbit](https://www.opswat.com/docs/mdss/integrations/add-a-cubbit-storage) | S3 Compatible | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Azure Blob](https://www.opswat.com/docs/mdss/integrations/add-an-azure-blob-storage) | Native | No | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | No |
| [Google Cloud](https://www.opswat.com/docs/mdss/integrations/add-a-google-cloud-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Alibaba Cloud](https://www.opswat.com/docs/mdss/integrations/add-an-alibaba-cloud-storage) | Native | No | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |

## File Storages

| Storage Name | Integration Type | Event-Based |
| ---- | ---- | ---- |
| [Box](https://www.opswat.com/docs/mdss/integrations/add-a-box-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-handling-for-box) |
| [OneDrive](https://www.opswat.com/docs/mdss/integrations/add-an-onedrive-storage) | Native | No |
| [SharePoint Online](https://www.opswat.com/docs/mdss/integrations/add-a-sharepoint-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-handling-for-sharepoint-online) |
| [Microsoft Teams](https://www.opswat.com/docs/mdss/integrations/add-a-microsoft-teams-storage) | Native | No |
| [SharePoint On-Premise](https://www.opswat.com/docs/mdss/integrations/add-a-sharepoint-on-premise-storage) | Native | No |
| [Azure Files](https://www.opswat.com/docs/mdss/integrations/add-an-azure-files-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) |
| [OPSWAT Managed File Transfer (MFT)](https://www.opswat.com/docs/mdss/integrations/add-a-mft-storage) | Native | No |

## Network Attached Storages (NAS)

| Storage Name | Integration Type | Event-Based | Delete empty folders |
| ---- | ---- | ---- | ---- |
| [NFS](https://www.opswat.com/docs/mdss/integrations/add-a-nfs-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | [Yes](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders) |
| [NFS with Data Wrapping](https://www.opswat.com/docs/mdss/integrations/add-an-nfs-with-data-wrapping-storage) | NFS | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | [Yes](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders) |
| [SMB](https://www.opswat.com/docs/mdss/integrations/add-a-smb-compatible-storage) | [NFS (recommended)](https://www.opswat.com/docs/mdss/integrations/how-to-add-a-smb-share-as-a-nfs-storage) Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | [Yes](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders) |
| [NetApp ONTAP](https://www.opswat.com/docs/mdss/integrations/add-a-netapp-ontap-storage) | SMB / NFS | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | [Yes](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders) |
| [Amazon EFS](https://www.opswat.com/docs/mdss/integrations/how-to-add-amazon-efs-as-a-nfs-storage-unit) | NFS | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | [Yes](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders) |
| [Dell Isilon](https://www.opswat.com/docs/mdss/integrations/add-a-dell-emc-isilon-storage) | SMB / NFS | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | [Yes](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders) |
| [SFTP](https://www.opswat.com/docs/mdss/integrations/add-a-sftp-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | [Yes](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders) |
| [FTP](https://www.opswat.com/docs/mdss/integrations/add-a-ftp-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | No |

*** Tags and checksum information**

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
