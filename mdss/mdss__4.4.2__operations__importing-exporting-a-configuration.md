<!-- source: https://www.opswat.com/docs/mdss/4.4.2/operations/importing-exporting-a-configuration -->

# Importing/Exporting a configuration

Importing a configuration file from a version greater than 4.0.0 that includes SSO settings will require reconfiguring SSO, as it was not properly exported.

MetaDefender Storage Security allows administrators to export and import system configuration files. This feature is useful for backup, migration, or replicating settings across environments.

## [Exporting the Configuration File](/docs/mdss/4.4.2/operations/importing-exporting-a-configuration#exporting-the-configuration-file)

On the **Settings page**, under the **Export tab**, you can export your system configuration. The export includes all system settings such as accounts, groups, storage units, scan pools, workflows, and more.

### [Steps to Export](/docs/mdss/4.4.2/operations/importing-exporting-a-configuration#steps-to-export)

1. Choose which parts of the configuration you want to export (License, SMTP settings, email notifications, retention settings).
2. In the Export Authentication section, you must set a password for the export operation. This password will be required to import the configuration file later. Please store it securely, as it cannot be recovered.
3. Click Export Configuration to download the configuration file. The file will be encrypted using the password you provided.

### [Export File Information](/docs/mdss/4.4.2/operations/importing-exporting-a-configuration#export-file-information)

1. Configurations from version 4.0.0 and newer are exported as ZIP files. Older versions use JSON format.
2. Export files typically range from 10MB for basic setups to 100MB+ for complex configurations.
3. Store export files in secure locations with appropriate access controls.

## [Importing a Configuration File](/docs/mdss/4.4.2/operations/importing-exporting-a-configuration#importing-a-configuration-file)

On a fresh install of MetaDefender Storage Security, after creating the first user account and logging in, you can choose to import an existing configuration.

### [Version Compatibility](/docs/mdss/4.4.2/operations/importing-exporting-a-configuration#version-compatibility)

- **JSON files** for configurations older than version 4.0.0
- **ZIP files** for configurations from version 4.0.0 or newer
- **Cross-version imports** for importing older configurations into newer versions - has limited compatibility and may require manual review

### [Steps to Import](/docs/mdss/4.4.2/operations/importing-exporting-a-configuration#steps-to-import)

In the Import Configuration screen, you can click on the input field, browse and select a file to Import. The input will accept either a JSON file (if the configuration is older than 4.0.0) or a .ZIP file (if the configuration is 4.0.0 or newer).

If the file is password-protected, you will be prompted to enter the password that was set during export. Afterwards, click on the Upload button and the configuration import procedure will start.

### [Import timing](/docs/mdss/4.4.2/operations/importing-exporting-a-configuration#import-timing)

The import process typically takes 30 seconds to 2 minutes, depending on configuration size. If license transfer is enabled, allow additional time for online activation.

### [Post-Import Requirements](/docs/mdss/4.4.2/operations/importing-exporting-a-configuration#post-import-requirements)

**Important**: After importing a configuration that contains advanced settings (such as HTTPS configurations, SSL certificates, or custom integrations), you must restart the following Windows services:

- MetaDefender Storage Security Service
- MetaDefender Storage Security Web Service
- MetaDefender Storage Security Scanning Service

**Note**: Service restart is only required if the imported configuration contains advanced settings. Basic configurations typically do not require a service restart.

### [Verification Steps](/docs/mdss/4.4.2/operations/importing-exporting-a-configuration#verification-steps)

After import completion, verify the following:

- All services are running properly
- License is activated (if applicable)
- Storage units are accessible
- User accounts function correctly
- Email notifications work (if configured)
