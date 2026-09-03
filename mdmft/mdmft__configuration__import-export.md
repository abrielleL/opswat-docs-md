<!-- source: https://www.opswat.com/docs/mdmft/configuration/import-export -->

# Import / Export

Summarize Page    Connect to Cursor Connect to VS Code

There are multiple items you can export from MetaDefender Managed File Transfer™.

## [Import and Export User Mapping Configuration](/docs/mdmft/configuration/import-export#import-and-export-user-mapping-configuration)

### [Import User Mapping Configuration](/docs/mdmft/configuration/import-export#import-user-mapping-configuration)

Administrators can edit [user mappings](/docs/mdmft/operating/user-mapping) in bulk. Save the user mapping configuration in a JSON file as shown below.

JsonCopy{
"$schema": "https://json-schema.org/draft/2020-12/schema",
"description": "List of users in MFT",
"type": "array",
"items": {
"description": "User",
"type": "object",
"properties": {
"type": {
"type": "string",
"enum": ["ActiveDirectory", "Local", "External", "Guest"]
},
"username": {
"type": "string",
"maxLength": 255,
"minLength": 1
},
"domain": {
"type": "string",
"maxLength": 255,
"minLength": 1
},
"email": {
"type": "string",
"format": "email",
"maxLength": 255,
"minLength": 1
},
"guest_pin": {
"type": "string",
"maxLength": 255,
"minLength": 1
},
"alteregos": {
"description": "List of users to be mapped to the current user",
"type": "array",
"items": {
"type": "object",
"properties": {
"type": {
"type": "string",
"enum": ["ActiveDirectory", "Local", "External", "Guest"]
},
"username": {
"type": "string",
"maxLength": 255,
"minLength": 1
},
"domain": {
"type": "string",
"maxLength": 255,
"minLength": 1
},
"email": {
"type": "string",
"format": "email",
"maxLength": 255,
"minLength": 1
},
"guest_pin": {
"type": "string",
"maxLength": 255,
"minLength": 1
}
},
"required": ["type"],
"oneOf": [
{
"properties": {
"type": { "const": "ActiveDirectory" }
},
"required": ["username"],
"not": {
"anyOf": [
{ "required": ["email"] },
{ "required": ["guest_pin"] }
]
}
},
{
"properties": {
"type": { "const": "Local" }
},
"anyOf": [
{ "required": ["username"] },
{ "required": ["email"] }
],
"not": {
"anyOf": [
{ "required": ["domain"] },
{ "required": ["guest_pin"] }
]
}
},
{
"properties": {
"type": { "const": "External" }
},
"anyOf": [
{ "required": ["username"] },
{ "required": ["email"] }
],
"not": {
"anyOf": [
{ "required": ["domain"] },
{ "required": ["guest_pin"] }
]
}
},
{
"properties": {
"type": { "const": "Guest" }
},
"required": ["guest_pin"],
"not": {
"anyOf": [
{ "required": ["username"] },
{ "required": ["domain"] },
{ "required": ["email"] }
]
}
}
]
}
}
},
"required": ["type"],
"oneOf": [
{
"properties": {
"type": { "const": "ActiveDirectory" }
},
"required": ["username"],
"not": {
"anyOf": [
{ "required": ["email"] },
{ "required": ["guest_pin"] }
]
}
},
{
"properties": {
"type": { "const": "Local" }
},
"anyOf": [
{ "required": ["username"] },
{ "required": ["email"] }
],
"not": {
"anyOf": [
{ "required": ["domain"] },
{ "required": ["guest_pin"] }
]
}
},
{
"properties": {
"type": { "const": "External" }
},
"anyOf": [
{ "required": ["username"] },
{ "required": ["email"] }
],
"not": {
"anyOf": [
{ "required": ["domain"] },
{ "required": ["guest_pin"] }
]
}
},
{
"properties": {
"type": { "const": "Guest" }
},
"required": ["guest_pin"],
"not": {
"anyOf": [
{ "required": ["username"] },
{ "required": ["domain"] },
{ "required": ["email"] }
]
}
}
]
}
}

Example for a user-mapping JSON file:

JsonCopy[
{
"type": "ActiveDirectory",
"username": "bob",
"domain": "ot",
"alteregos": [
{
"type": "ActiveDirectory",
"username": "bobby",
"domain": "itnetwork"
},
{
"type": "Local",
"username": "bob",
"email": "bob@mail.com"
}
]
},
{
"type": "Local",
"username": "ted",
"alteregos": [
{
"type": "Guest",
"guest_pin": "K+sgvh8LqTa6"
},
{
"type": "ActiveDirectory",
"username": "ted",
"domain": "itnetwork"
}
]
}
]

To import user mapping data:

1. In the Import User Mapping section, click Browse to select the configuration file
2. Click Import User Mapping to start the import process
3. A notification will appear confirming the result of the import
4. To verify imported mappings, navigate to Users → Local Users, External Users, etc., under the Users submenu

### [Export User Mapping Configuration](/docs/mdmft/configuration/import-export#export-user-mapping-configuration)

Administrators can export the current user mapping configuration as a JSON file. (See example below.)

## [Export User List](/docs/mdmft/configuration/import-export#export-user-list)

Administrators can export user information in CSV format. A password is required to complete the export process. Exported values include:

- User ID
- Username
- User Status
- Creation Time
- Email
- Notification Email
- Role
- Last Login
- Phone Number

Finish it by click "Export". The CSV file will be in the password-protected UserList.zip file.

## [Import and Export MFT Configuration](/docs/mdmft/configuration/import-export#import-and-export-mft-configuration)

Clone the configuration of a MetaDefender Managed File Transfer installation by exporting the configuration file into a zip archive, then extracting and importing it on another instance.

The exported configuration includes:

- Global settings
- Core integration
- Active Directories
- Supervisor approval
- Outbreak prevention
- Language
- SMTP
- Email templates
- Logging
- Syslog settings
- Trusted Networks
- Recycle Bin settings

### [Export Options and Considerations](/docs/mdmft/configuration/import-export#export-options-and-considerations)

**Perform License Transfer** (optional): If selected, any online-activated license will be deactivated during export. When the configuration is imported on another machine, the license will be automatically reactivated.

**Archive Password** (optional): You can define an Archive Password to protect the exported configuration archive.

Info

Only configuration data will be exported. User accounts, user files, API keys, audit log, and other instance-specific data will not be included.

Configuration related to HTTPS is not exported or imported. After import, follow the [**Security**](/docs/mdmft) instructions to switch to HTTPS.

Info

If an Active Directory (AD) group is part of a Trusted Network rule, it will be included in the export. However, if the associated AD is removed after export, the group will not be re-imported unless the AD integration is re-established beforehand.

### [Exporting the Current Configuration](/docs/mdmft/configuration/import-export#exporting-the-current-configuration)

1. Log in as an Administrator to MetaDefender Managed File Transfer
2. Navigate to Settings → Import/Export
3. Click the Export Configuration button
4. Save the exported configuration file to your local disk

### [Importing Configuration from Another Installation](/docs/mdmft/configuration/import-export#importing-configuration-from-another-installation)

1. Log in as an Administrator to MetaDefender Managed File Transfer
2. Go to "Settings" → "Import"/"Export"
3. Click "Browse" to upload the previously exported configuration file or the ZIP archive
4. If the ZIP file is password-protected, enter the password
5. Click "Import Configuration" to begin the process
6. Once the import is complete, a notification message will appear

To complete the configuration, go to "Windows Services" and restart the following MetaDefender Managed File Transfer services.

1. OPSWAT MetaDefender Managed File Transfer Helper
2. OPSWAT MetaDefender Managed File Transfer Processor
3. OPSWAT MetaDefender Managed File Transfer REST
4. OPSWAT MetaDefender Managed File Transfer Next

Info

Restarting services is required if the exported configuration includes changes to any .config files (e.g., HTTPS). If no such changes are present, restarting services is not necessary.

Info

The import process may take several seconds, especially if license reactivation occurs (e.g. when the "Perform license transfer" option was selected during export). Wait for the completion notification before any further actions in the system.
