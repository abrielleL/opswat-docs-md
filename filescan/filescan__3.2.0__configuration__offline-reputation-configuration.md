<!-- source: https://www.opswat.com/docs/filescan/3.2.0/configuration/offline-reputation-configuration -->

# Offline Reputation Service

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The **Offline** **Reputation Service** allows your organization to influence threat decisions by managing known good and bad files and indicators. You can supply your own local reputation data, and our system also includes managed reputation entries out of the box.

Info

This feature is available since version `2.3.0`.

Pro Tip

Use comments in your reputation files to keep track of sources—just add a description after a comma!

## [Supported Data Types](/docs/filescan/3.2.0/configuration/offline-reputation-configuration#supported-data-types)

Sandbox supports reputation entries for the following data types:

- `md5` – File hash (32-character)
- `sha256` – File hash (64-character)
- `ip` – IPv4 or IPv6 addresses
- `domain` – Network domain names
- `url` – Full URLs
- `digicert_owner` – Digital Certificate owners (common name / organization)

Each entry can be part of either an **allow list** or a **block list**, to determine whether files or indicators (IOCs) should be trusted or flagged.

Note

Only **allowed** entries are supported for Digital Certificate owners.

Warning

Sandbox cannot verify **certificates** in **offline environments**, therefore the certificate allowlist is ignored for allow listing.

## [Directory Structure](/docs/filescan/3.2.0/configuration/offline-reputation-configuration#directory-structure)

Reputation data is stored in the following directories:

- **System-managed data**: has been removed from directory structure, it is a part of the detection package
- **Customer-provided data**: `<sandbox>/transform/data/reputation/external`(Customers can edit and manage this at any time)

Note

Customer managed data takes precedence on conflict.

## [File Naming Convention](/docs/filescan/3.2.0/configuration/offline-reputation-configuration#file-naming-convention)

Customers can provide their reputation data in files following this naming format:

| Data Type | Allow list file | Block list file |
| --- | --- | --- |
| MD5 | md5_allowed.txt | md5_blocked.txt |
| SHA256 | `sha256_allowed.txt` | sha256_blocked.txt |
| IP | ip_allowed.txt | ip_blocked.txt |
| Domain | domain_allowed.txt | domain_blocked.txt |
| URL | url_allowed.txt | url_blocked.txt |
| Digital Certificate owner | digicert_owner_allowed.txt | *(no block list supported)* |

## [File Format](/docs/filescan/3.2.0/configuration/offline-reputation-configuration#file-format)

Each file - except `digicert_owner_allowed.txt` - can contain single line entries as comma separated data and optional description pairs.

CsvCopy<data>,<optional description>

Examples:

md5_allowed.txtCopyd41d8cd98f00b204e9800998ecf8427e,Known good from internal tool, empty file
d41d8cd98f00b204e9800998ecf8427dWarning

For `digicert_owner_allowed.txt`, description is not supported.

Example:

digicert_owner_allowed.txtCopyCN="Trusted .Inc", O="Trusted, Inc.", L=San Francisco, ST=California, C=US
## [Import Behavior](/docs/filescan/3.2.0/configuration/offline-reputation-configuration#import-behavior)

- Data is **imported at application startup**, **if a file has changed**.
- If a file changes, **existing data for that type and list is replaced entirely**.
- All internal (system-managed) reputation data is updated after installation.
- External (customer) reputation data can be modified and re-imported at any time.

Note

Restart Sandbox to trigger the data import

BashCopysudo service sandbox restart
## [Validation and Logs](/docs/filescan/3.2.0/configuration/offline-reputation-configuration#validation-and-logs)

- All entries are **validated** during import based on type.
- **Invalid entries are skipped silently**.
- To ensure full effectiveness, customers advised to **check the logs** for any skipped entries or formatting errors.

Example transform logs for successful import and migration with an invalid data entry:

Warning

It is advised to **check the logs** for any skipped entries or formatting errors.

INFO Starting reputation data migration...
INFO External reputation data migration completed successfully
INFO Reloading reputation data from file: /home/akos/workspace/sandbox/fstransform/data/reputation/internal/md5_allowed.txt
INFO Reloaded 1736511 entries from changed file: md5_allowed.txt
...
INFO Reloading reputation data from file: <sandbox>/fstransform/data/reputation/internal/ip_blocked.txt
ERROR Failed to parse reputation data line: Invalid IP format. Must be a valid IPv4 or IPv6 address: 212.111.1.212.226
INFO Reloaded 455823 entries from changed file: ip_blocked.txt
INFO Reloading reputation data from file: <sandbox>/fstransform/data/reputation/internal/url_allowed.txt
INFO Reloaded 18 entries from changed file: url_allowed.txt
## [Migration of Old External Data](/docs/filescan/3.2.0/configuration/offline-reputation-configuration#migration-of-old-external-data)

- Legacy external reputation data is **automatically migrated** during the first startup after the installation of `version 2.3.0` or later.
- A **migration marker file** indicates completion of the migration step: <sandbox>/transform/data/reputation/external/.reputation_migration_completed

## [Additional Allow List Behavior](/docs/filescan/3.2.0/configuration/offline-reputation-configuration#additional-allow-list-behavior)

- **URL Matching**: A URL is allowed or blocked based on its **domain's** presence in the allow/block list.
- **IP Matching**: An IP is considered **allowed** if it:

  - Matches exactly
  - Is a **network address** - see transform configuration setting `ignoreNetworkIPs`
  - Is a **broadcast** **address** - see transform configuration setting `ignoreBroadcastIPs`
  - Falls within an **allowed subnet** - see transform configuration setting `whitelistHostsCIDR`

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
