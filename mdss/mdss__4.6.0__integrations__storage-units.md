<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/storage-units -->

# Integrations

MetaDefender Storage Security integrates with various cloud and on-premises storage solutions, represented as **storage units**.

We provide a list (see table below) of officially supported integrations that are continuously tested for full functionality.

> **IMPORTANT Please get in touch with us if your specific storage provider isn't shown.**
>
> We likely already support storage systems that use S3-compatible interfaces or standard protocols such as SMB, NFS, or SFTP.

## Cloud Object Storages

| Storage Name | Integration Type | Tagging | Event-Based | Metadata Copy | Autodiscovery |
| ---- | ---- | ---- | ---- | ---- | ---- |
| [Amazon S3](https://www.opswat.com/docs/mdss/integrations/add-an-amazon-s3-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-aws-example) | Yes | [Yes](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-amazon-s3) |
| [Wasabi](https://www.opswat.com/docs/mdss/integrations/add-a-wasabi-storage) | S3 Compatible | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | Yes | [Yes](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-amazon-s3) |
| [Cloudian®](https://www.opswat.com/docs/mdss/integrations/add-a-cloudian-storage) | S3 Compatible | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | Yes | [Yes](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-amazon-s3) |
| [Oracle Cloud](https://www.opswat.com/docs/mdss/integrations/add-an-oracle-cloud-storage) | S3 Compatible | No | No | Yes | [Yes](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-amazon-s3) |
| [Oracle Cloud](https://www.opswat.com/docs/mdss/integrations/add-an-oracle-sdk-storage) | Native | No | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-handling-for-oraclesdk) | Yes | No |
| [MinIO](https://www.opswat.com/docs/mdss/integrations/add-a-minio-storage) | S3 Compatible | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | Yes | [Yes](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-amazon-s3) |
| [Cubbit](https://www.opswat.com/docs/mdss/integrations/add-a-cubbit-storage) | S3 Compatible | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | No | Yes | [Yes](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-amazon-s3) |
| [Azure Blob](https://www.opswat.com/docs/mdss/integrations/add-an-azure-blob-storage) | Native | No | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-handling-for-azure) | No | [Yes](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-azure-blob) |
| [Google Cloud](https://www.opswat.com/docs/mdss/integrations/add-a-google-cloud-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No | [Yes](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-google-cloud) |
| [Alibaba Cloud](https://www.opswat.com/docs/mdss/integrations/add-an-alibaba-cloud-storage) | Native | No | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | No | No |
| [Scality RING](https://www.opswat.com/docs/mdss/integrations/add-a-scality-ring-storage) | S3 Compatible | [Yes](https://www.opswat.com/docs/mdss/configuration/file-tagging) | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) | Yes | [Yes](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-amazon-s3) |

## File Storages

| Storage Name | Integration Type | Event-Based | Autodiscovery | Replace Original | Scan File Versions |
| ---- | ---- | ---- | ---- | ---- | ---- |
| [Box](https://www.opswat.com/docs/mdss/integrations/add-a-box-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-handling-for-box) | No | No | No |
| [OneDrive](https://www.opswat.com/docs/mdss/integrations/add-an-onedrive-storage) | Native | No | No | [Yes](https://www.opswat.com/docs/mdss/configuration/deep-content-disarm-and-reconstruction--deep-cdr-#replace-original-files-with-sanitized-versions) | No |
| [SharePoint Online](https://www.opswat.com/docs/mdss/integrations/add-a-sharepoint-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-handling-for-sharepoint-online) | [Yes](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-sharepoint-online) | [Yes](https://www.opswat.com/docs/mdss/configuration/deep-content-disarm-and-reconstruction--deep-cdr-#replace-original-files-with-sanitized-versions) | No |
| [Microsoft Teams](https://www.opswat.com/docs/mdss/integrations/add-a-microsoft-teams-storage) | Native | No | No | [Yes](https://www.opswat.com/docs/mdss/configuration/deep-content-disarm-and-reconstruction--deep-cdr-#replace-original-files-with-sanitized-versions) | No |
| [SharePoint On-Premise](https://www.opswat.com/docs/mdss/integrations/add-a-sharepoint-on-premise-storage) | Native | No | No | No | [Yes](https://www.opswat.com/docs/mdss/configuration/scan-file-versions) |
| [Azure Files](https://www.opswat.com/docs/mdss/integrations/add-an-azure-files-storage) | Native | No | No | No | No |
| [OPSWAT Managed File Transfer (MFT)](https://www.opswat.com/docs/mdss/integrations/add-a-mft-storage) | Native | No | No | No | No |

## Network Attached Storages (NAS)

| Storage Name | Integration Type | Event-Based | Delete empty folders | Autodiscovery |
| ---- | ---- | ---- | ---- | ---- |
| [NFS](https://www.opswat.com/docs/mdss/integrations/add-a-nfs-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | [Yes](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders) | No |
| [NFS with Data Wrapping](https://www.opswat.com/docs/mdss/integrations/add-an-nfs-with-data-wrapping-storage) | NFS | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | No | No |
| [SMB](https://www.opswat.com/docs/mdss/integrations/add-a-smb-compatible-storage) | [NFS (recommended)](https://www.opswat.com/docs/mdss/integrations/how-to-add-a-smb-share-as-a-nfs-storage) Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | [Yes](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders) | No |
| [NetApp ONTAP](https://www.opswat.com/docs/mdss/integrations/add-a-netapp-ontap-storage) | SMB | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | No | No |
| [Amazon EFS](https://www.opswat.com/docs/mdss/integrations/how-to-add-amazon-efs-as-a-nfs-storage-unit) | NFS | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | [Yes](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders) | No |
| [Dell Isilon](https://www.opswat.com/docs/mdss/integrations/add-a-dell-emc-isilon-storage) | SMB | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | No | No |
| [SFTP](https://www.opswat.com/docs/mdss/integrations/add-a-sftp-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | [Yes](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders) | No |
| [FTP](https://www.opswat.com/docs/mdss/integrations/add-a-ftp-storage) | Native | [Yes](https://www.opswat.com/docs/mdss/configuration/event-based-request-format) | No | No |

### **Extra functionalities**

> **How Replace Original works**
>
> With [Replace Original](https://www.opswat.com/docs/mdss/configuration/deep-content-disarm-and-reconstruction--deep-cdr-#replace-original-files-with-sanitized-versions) enabled, MetaDefender Storage Security overwrites the content of the original file with the sanitized content. No new file is created: the file keeps its name, location and sharing, so users keep opening the same file and now get the sanitized version.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
