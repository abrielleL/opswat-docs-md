<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/custom-configuration -->

# Custom configuration

## How to edit the configuration file on Linux

Custom application configuration can be achieved by editing the *customer.env* environment file.

The following steps are required to change different parameters in this file:

- Navigate to */etc/mdss/customer.env* and open the file
- If the parameter that needs to be changed is not present, add the new parameter with the desired value. If it already exists, just edit the value.

```plaintext
CONFIGURATION_PROPERTY_NAME=VALUE
```

- Save the file
- In order for the changes to apply, please restart the application by running the following command:

```plaintext
sudo mdss -c restart
```

## How to edit the configuration file on Windows

Custom application configuration can be achieved by editing the *customer.env* environment file.

The following steps are required to change different parameters in this file:

- By default the file is located in C:\Program Files\OPSWAT\MetaDefender Storage Security\config\cutomer.env
- If the parameter that needs to be changed is not present, add the new parameter with the desired value. If it already exists, just edit the value

```plaintext
CONFIGURATION_PROPERTY_NAME=VALUE
```

- Save the file
- In order for the changes to apply, please restart the application by running the following command:

```plaintext
mdss.ps1 -c refresh
```

## Increase the number of concurrent scans

To be able to scan multiple files at the same time, the event bus needs to be configured accordingly. Please add the following environment variable in your *customer.env* file (as described above):

| **Environment Variable** | **Default Value** | **Maximum Value** | **Description** |
| ---- | ---- | ---- | ---- |
| RABBITMQ_SCANNING_PREFETCH_COUNT | 20 | 200 | Allow up to 50 files to be scanned at the same time. |

## Certificate validation for MetaDefender Core connection

This environment variable controls certificate validation for MetaDefender Core integration during HTTP(S) requests. It is useful when MetaDefender Storage Security needs to accept a partially valid certificate chain or a self-signed certificate.

| Environment Variable | Default Value | Possible Values |
| ---- | ---- | ---- |
| MD_CORE_CERTIFICATE_VALIDATION | 0 | 0 - Use the built-in validation (recommended) 1 - Ignore certificate chain errors 2 - Ignore all certificate errors |

#### Description

- 0 → A MetaDefender Core server with invalid certificate can't be integrated
- 1 → A MetaDefender Core server with certificate chain errors can be integrated
- 2 → A MetaDefender Core server with invalid certificate can be integrated

## MetaDefender Core unavailability period

Configure the period of time a MetaDefender Core server is considered unavailable when a scan failure occurs.

| Environment Variable | Default Value | Description |
| ---- | ---- | ---- |
| LOAD_BALANCER_MD_CORE_UNAVAILABLE_TIME | 5 | When a scan fails, the respective MetaDefender Core server will be unavailable for this period of time (in minutes). The load balancer cannot choose it for another file during this time period. |

## Azure Blobs

Configure the number of blobs read in one request

| Environment Variable | Default Value | Max Value | Description |
| ---- | ---- | ---- | ---- |
| AZURE_BLOB_PAGE_SIZE | 100 | 5000 | Number of blobs discovered in container in a single request. |

## Amazon S3

Configure the validity duration of presigned URL used for download files from storage

| Environment Variable | Default Value | Min Value | Description |
| ---- | ---- | ---- | ---- |
| PRESIGNED_URL_EXPIRATION_SECONDS | 259200 | 30 | Value is defined in seconds |

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
