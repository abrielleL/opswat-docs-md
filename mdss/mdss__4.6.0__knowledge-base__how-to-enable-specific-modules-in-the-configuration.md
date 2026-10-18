<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/how-to-enable-specific-modules-in-the-configuration -->

# How to Enable Specific Modules in the Configuration?

## Enabling Modules

`ENABLED_MODULES` in `customer.env` lists the storage types this deployment offers. It is the product-level feature gate: storage types of modules not listed still appear in the user interface, but they are disabled and cannot be selected when an account is added.

For instance, if your purpose is to scan Amazon S3 buckets only, keep just the `amazonsdk` module in `ENABLED_MODULES`:

```bash
ENABLED_MODULES=amazonsdk
```

Please follow [Custom configuration](https://www.opswat.com/docs/mdss/configuration/custom-configuration) to learn how to modify the `customer.env`  file.

It's important to remember that turning modules on or off is a non-destructive action, allowing you the flexibility to activate additional modules later if you need to work with different types of storage.

By default, all modules are enabled, which means that `ENABLED_MODULES` will look like this right after the installation:

```bash
ENABLED_MODULES=azureblob,amazonsdk,googlecloud,alibabacloud,azurefiles,smb,box,graph,sftp,nfs,mft,ftp,oraclesdk
```

| Module | Storage types |
| ---- | ---- |
| `amazonsdk` | Amazon S3 and the S3-compatible storages (S3 Compatible, Wasabi, Oracle S3-Compatible, Cubbit, Scality RING) |
| `azureblob` | Azure Blob |
| `azurefiles` | Azure Files |
| `googlecloud` | Google Cloud Storage |
| `alibabacloud` | Alibaba Cloud OSS |
| `oraclesdk` | Oracle Cloud Storage |
| `box` | Box |
| `graph` | SharePoint Online and OneDrive (Microsoft Graph). Replaces the former `onedrive` module name |
| `sftp` | SFTP |
| `ftp` | FTP |
| `mft` | MetaDefender Managed File Transfer |
| `nfs` | NFS and NFS with Data Wrapping |
| `smb` | SMB / CIFS, including Dell Isilon and NetApp ONTAP shares |

`smb_legacy` is an additional module for Linux deployments. It selects the previous SMB service for hosts that cannot run the SMB service's kernel mount; keep `smb` in the list and add `smb_legacy` at the end. See [Add an SMB-Compatible unit in Linux deployments](https://www.opswat.com/docs/mdss/integrations/how-to-add-a-smb-share-as-a-nfs-storage).

Use the module names exactly as listed above. Names are case-sensitive and must be separated by commas without spaces. Unknown module names are ignored, and the corresponding integrations are not available. Before upgrading, review your list as described in [Upgrade MDSS](https://opswat.developerhub.io/docs/mdss/installation/upgrade-procedures).

Please change it accordingly but remember that in order for these changes to be applied you need to restart MetaDefender Storage Security.

> **Resource usage**
>
> Disabling a module other than `nfs` or `smb` does not reduce the number of containers. Every storage type except NFS and SMB runs in-process inside the central Storages, Discovery, Remediations and Scanning services, so no container is started or stopped when it is enabled or disabled. Only `nfs` and `smb` add a container each (`mdintegrations_nfsservice`, `mdintegrations_smbservice`); removing them from `ENABLED_MODULES` also removes those containers.
>
> An upgraded installation keeps the `ENABLED_MODULES` value it had before the upgrade.

## Disabling Services

The following services can be disabled when they are managed externally, to prevent deploying their local container versions:

- MongoDB
- PostgreSQL
- RabbitMQ
- Redis

They can be disabled by adding them individually to the `DISABLED_SERVICES`  variable in `customer.env` :

```bash
DISABLED_SERVICES=mongo,postgres,rabbitmq,redis
```

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
