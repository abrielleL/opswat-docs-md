<!-- source: https://www.opswat.com/docs/mdss/integrations/storage-units -->

# Integrations

MetaDefender Storage Security integrates with various cloud and on-premises storage solutions, represented as **storage units**.

We provide a list (see table below) of officially supported integrations that are continuously tested for full functionality.

IMPORTANT
Please get in touch with us if your specific storage provider isn't shown.

We likely already support storage systems that use S3-compatible interfaces or standard protocols such as SMB, NFS, or SFTP.

## [Cloud Object Storages](/docs/mdss/integrations/storage-units#cloud-object-storages)

| Storage Name | Integration Type | Tagging | Event-Based | Metadata * Copy |
| --- | --- | --- | --- | --- |
| [Amazon S3](/docs/mdss/integrations/add-an-amazon-s3-storage) | Native | [Yes](/docs/mdss/configuration/file-tagging) | [Yes](/docs/mdss/configuration/event-based-real-time-aws-example) | Yes |
| [Wasabi](/docs/mdss/integrations/add-a-wasabi-storage) | S3 Compatible | [Yes](/docs/mdss/configuration/file-tagging) | [Yes](/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Cloudian®](/docs/mdss/integrations/add-a-cloudian-storage) | S3 Compatible | [Yes](/docs/mdss/configuration/file-tagging) | [Yes](/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Oracle Cloud](/docs/mdss/integrations/add-an-oracle-cloud-storage) | S3 Compatible | [Yes](/docs/mdss/configuration/file-tagging) | [Yes](/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Oracle Cloud](/docs/mdss/integrations/add-an-oracle-sdk-storage) | Native | No | [Yes](/docs/mdss/configuration/event-based-real-time-handling-for-oraclesdk) | Yes |
| [MinIO](/docs/mdss/integrations/add-a-minio-storage) | S3 Compatible | [Yes](/docs/mdss/configuration/file-tagging) | [Yes](/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Cubbit](/docs/mdss/integrations/add-a-cubbit-storage) | S3 Compatible | [Yes](/docs/mdss/configuration/file-tagging) | [Yes](/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Azure Blob](/docs/mdss/integrations/add-an-azure-blob-storage) | Native | No | [Yes](/docs/mdss/configuration/event-based-request-format) | No |
| [Google Cloud](/docs/mdss/integrations/add-a-google-cloud-storage) | Native | [Yes](/docs/mdss/configuration/file-tagging) | [Yes](/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Alibaba Cloud](/docs/mdss/integrations/add-an-alibaba-cloud-storage) | Native | No | [Yes](/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No |

## [File Storages](/docs/mdss/integrations/storage-units#file-storages)

| Storage Name | Integration Type | Event-Based |
| --- | --- | --- |
| [Box](/docs/mdss/integrations/add-a-box-storage) | Native | [Yes](/docs/mdss/configuration/event-based-handling-for-box) |
| [OneDrive](/docs/mdss/integrations/add-an-onedrive-storage) | Native | No |
| [SharePoint Online](/docs/mdss/integrations/add-a-sharepoint-storage) | Native | [Yes](/docs/mdss/configuration/event-based-handling-for-sharepoint-online) |
| [Microsoft Teams](/docs/mdss/integrations/add-a-microsoft-teams-storage) | Native | No |
| [SharePoint On-Premise](/docs/mdss/integrations/add-a-sharepoint-on-premise-storage) | Native | No |
| [Azure Files](/docs/mdss/integrations/add-an-azure-files-storage) | Native | [Yes](/docs/mdss/configuration/event-based-request-format) |
| [OPSWAT Managed File Transfer (MFT)](/docs/mdss/integrations/add-a-mft-storage) | Native | No |

## [Network Attached Storages (NAS)](/docs/mdss/integrations/storage-units#network-attached-storages-nas)

| Storage Name | Integration Type | Event-Based | Delete empty folders |
| --- | --- | --- | --- |
| [NFS](/docs/mdss/integrations/add-a-nfs-storage) | Native | [Yes](/docs/mdss/configuration/event-based-request-format) | [Yes](/docs/mdss/configuration/delete-empty-folders) |
| [SMB](/docs/mdss/integrations/add-a-smb-compatible-storage) | [NFS (recommended)](/docs/mdss/integrations/how-to-add-a-smb-share-as-a-nfs-storage)  Native | [Yes](/docs/mdss/configuration/event-based-request-format) | [Yes](/docs/mdss/configuration/delete-empty-folders) |
| [NetApp ONTAP](/docs/mdss/integrations/add-a-netapp-ontap-storage) | SMB / NFS | [Yes](/docs/mdss/configuration/event-based-request-format) | [Yes](/docs/mdss/configuration/delete-empty-folders) |
| [Amazon EFS](/docs/mdss/integrations/how-to-add-amazon-efs-as-a-nfs-storage-unit) | NFS | [Yes](/docs/mdss/configuration/event-based-request-format) | [Yes](/docs/mdss/configuration/delete-empty-folders) |
| [Dell Isilon](/docs/mdss/integrations/add-a-dell-emc-isilon-storage) | SMB / NFS | [Yes](/docs/mdss/configuration/event-based-request-format) | [Yes](/docs/mdss/configuration/delete-empty-folders) |
| [SFTP](/docs/mdss/integrations/add-a-sftp-storage) | Native | [Yes](/docs/mdss/configuration/event-based-request-format) | [Yes](/docs/mdss/configuration/delete-empty-folders) |
| [FTP](/docs/mdss/integrations/add-a-ftp-storage) | Native | [Yes](/docs/mdss/configuration/event-based-request-format) | No |

*** Tags and checksum information**
