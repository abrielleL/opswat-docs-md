<!-- source: https://www.opswat.com/docs/mdss/4.5.2/knowledge-base/how-to-enable-specific-modules-in-the-configuration -->

# How to Enable Specific Modules in the Configuration?

## Enabling Modules

During the [installation](https://www.opswat.com/docs/mdss/installation/installation-methods) it is advisable to activate only those modules you intend to use, as a measure to conserve resources.

For instance, if your purpose is to scan Amazon S3 buckets, then you should only have the `amazonsdk` module enabled in `ENABLED_MODULES` environment variable inside the `customer.env` file.

```bash
ENABLED_MODULES=amazonsdk
```

Please follow [Custom configuration](https://www.opswat.com/docs/mdss/configuration/custom-configuration) to learn how to modify the `customer.env`  file.

It's important to remember that turning modules on or off is a non-destructive action, allowing you the flexibility to activate additional modules later if you need to work with different types of storage.

By default, all modules are enabled, which means that `ENABLED_MODULES` will look like this right after the installation:

```bash
ENABLED_MODULES=azureblob,amazonsdk,googlecloud,alibabacloud,azurefiles,smb,box,onedrive,sftp,nfs
```

Please change it accordingly but remember that in order for these changes to be applied you need to restart MetaDefender Storage Security.

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
