<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/storage-units -->

# Integrations

MetaDefender Storage Security integrates with various cloud and on-premises storage solutions, represented as **storage units**.

We provide a list (see table below) of officially supported integrations that are continuously tested for full functionality.

IMPORTANT
Please get in touch with us if your specific storage provider isn't shown.

We likely already support storage systems that use S3-compatible interfaces or standard protocols such as SMB, NFS, or SFTP.

## [Cloud Object Storages](/docs/mdss/4.4.2/integrations/storage-units#cloud-object-storages)

| Storage Name | Integration Type | Tagging | Event-Based | Metadata * Copy |
| --- | --- | --- | --- | --- |
| [Amazon S3](/docs/mdss/4.4.2/integrations/add-an-amazon-s3-storage) | Native | [Yes](/docs/mdss/4.4.2/configuration/file-tagging) | [Yes](/docs/mdss/4.4.2/configuration/event-based-real-time-aws-example) | Yes |
| [Wasabi](/docs/mdss/4.4.2/integrations/add-a-wasabi-storage) | S3 Compatible | [Yes](/docs/mdss/4.4.2/configuration/file-tagging) | [Yes](/docs/mdss/4.4.2/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Cloudian®](/docs/mdss/4.4.2/integrations/add-a-cloudian-storage) | S3 Compatible | [Yes](/docs/mdss/4.4.2/configuration/file-tagging) | [Yes](/docs/mdss/4.4.2/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Oracle Cloud](/docs/mdss/4.4.2/integrations/add-an-oracle-cloud-storage) | S3 Compatible | [Yes](/docs/mdss/4.4.2/configuration/file-tagging) | [Yes](/docs/mdss/4.4.2/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Oracle Cloud](/docs/mdss/4.4.2/metadefender-storage-security/4.3.0/integrations/add-an-oracle-cloud-storage) | Native | No | [Yes](/docs/mdss/4.4.2/metadefender-storage-security/4.3.0/configuration/event-based-real-time-handling-for-oraclesdk) | Yes |
| [MinIO](/docs/mdss/4.4.2/integrations/add-a-minio-storage) | S3 Compatible | [Yes](/docs/mdss/4.4.2/configuration/file-tagging) | [Yes](/docs/mdss/4.4.2/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Cubbit](/docs/mdss/4.4.2/integrations/add-a-cubbit-storage) | S3 Compatible | [Yes](/docs/mdss/4.4.2/configuration/file-tagging) | [Yes](/docs/mdss/4.4.2/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Azure Blob](/docs/mdss/4.4.2/integrations/add-an-azure-blob-storage) | Native | No | [Yes](/docs/mdss/4.4.2/configuration/event-based-request-format) | No |
| [Google Cloud](/docs/mdss/4.4.2/integrations/add-a-google-cloud-storage) | Native | [Yes](/docs/mdss/4.4.2/configuration/file-tagging) | [Yes](/docs/mdss/4.4.2/configuration/event-based-real-time-cloud-functions-examples) | No |
| [Alibaba Cloud](/docs/mdss/4.4.2/integrations/add-an-alibaba-cloud-storage) | Native | No | [Yes](/docs/mdss/4.4.2/configuration/event-based-real-time-cloud-functions-examples) | No |

## [File Storages](/docs/mdss/4.4.2/integrations/storage-units#file-storages)

| Storage Name | Integration Type | Event-Based |
| --- | --- | --- |
| [Box](/docs/mdss/4.4.2/integrations/add-a-box-storage) | Native | [Yes](/docs/mdss/4.4.2/configuration/event-based-handling-for-box) |
| [OneDrive](/docs/mdss/4.4.2/integrations/add-an-onedrive-storage) | Native | No |
| [SharePoint Online](/docs/mdss/4.4.2/integrations/add-a-sharepoint-storage) | Native | [Yes](/docs/mdss/4.4.2/configuration/event-based-handling-for-sharepoint-online) |
| [Microsoft Teams](/docs/mdss/4.4.2/metadefender-storage-security/4.3.0/integrations/add-a-microsoft-teams-storage) | Native | No |
| [SharePoint On-Premise](/docs/mdss/4.4.2/integrations/add-a-sharepoint-on-premise-storage) | Native | No |
| [Azure Files](/docs/mdss/4.4.2/integrations/add-an-azure-files-storage) | Native | [Yes](/docs/mdss/4.4.2/configuration/event-based-request-format) |
| [OPSWAT Managed File Transfer (MFT)](/docs/mdss/4.4.2/integrations/add-a-mft-storage) | Native | No |

## [Network Attached Storages (NAS)](/docs/mdss/4.4.2/integrations/storage-units#network-attached-storages-nas)

| Storage Name | Integration Type | Event-Based | Delete empty folders |
| --- | --- | --- | --- |
| [NFS](/docs/mdss/4.4.2/integrations/add-a-nfs-storage) | Native | [Yes](/docs/mdss/4.4.2/configuration/event-based-request-format) | [Yes](/docs/mdss/4.4.2/configuration/delete-empty-folders) |
| [SMB](/docs/mdss/4.4.2/integrations/add-a-smb-compatible-storage) | [NFS (recommended)](/docs/mdss/4.4.2/integrations/how-to-add-a-smb-share-as-a-nfs-storage)  Native | [Yes](/docs/mdss/4.4.2/configuration/event-based-request-format) | [Yes](/docs/mdss/4.4.2/configuration/delete-empty-folders) |
| [NetApp ONTAP](/docs/mdss/4.4.2/integrations/add-a-netapp-ontap-storage) | SMB / NFS | [Yes](/docs/mdss/4.4.2/configuration/event-based-request-format) | [Yes](/docs/mdss/4.4.2/configuration/delete-empty-folders) |
| [Amazon EFS](/docs/mdss/4.4.2/integrations/how-to-add-amazon-efs-as-a-nfs-storage-unit) | NFS | [Yes](/docs/mdss/4.4.2/configuration/event-based-request-format) | [Yes](/docs/mdss/4.4.2/configuration/delete-empty-folders) |
| [Dell Isilon](/docs/mdss/4.4.2/integrations/add-a-dell-emc-isilon-storage) | SMB / NFS | [Yes](/docs/mdss/4.4.2/configuration/event-based-request-format) | [Yes](/docs/mdss/4.4.2/configuration/delete-empty-folders) |
| [SFTP](/docs/mdss/4.4.2/integrations/add-a-sftp-storage) | Native | [Yes](/docs/mdss/4.4.2/configuration/event-based-request-format) | [Yes](/docs/mdss/4.4.2/configuration/delete-empty-folders) |
| [FTP](/docs/mdss/4.4.2/integrations/add-a-ftp-storage) | Native | [Yes](/docs/mdss/4.4.2/configuration/event-based-request-format) | No |

*** Tags and checksum information**
