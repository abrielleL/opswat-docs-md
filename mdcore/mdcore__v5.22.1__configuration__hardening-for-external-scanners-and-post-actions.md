<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/hardening-for-external-scanners-and-post-actions -->

# Hardening External Scanner and Post Action feature

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Since MetaDefender Core v5.14.1, we have introduced a security hardening feature that allows administrators to restrict which commands can be used in External Scanners and Post Actions. This guide will help you set up and configure that external command allowlist.

## [Benefits of Command Allowlisting](/docs/mdcore/v5.22.1/configuration/hardening-for-external-scanners-and-post-actions#benefits-of-command-allowlisting)

- **Enhanced Security**: Prevents the execution of unauthorized or potentially harmful commands
- **Controlled Environment**: Ensures only approved commands are used in your workflow
- **Compliance**: Helps meet security requirements by restricting command execution

## [Setting Up the External Allowlist](/docs/mdcore/v5.22.1/configuration/hardening-for-external-scanners-and-post-actions#setting-up-the-external-allowlist)

### [File Location](/docs/mdcore/v5.22.1/configuration/hardening-for-external-scanners-and-post-actions#file-location)

Create a new JSON file named `external_allowlist.json` in the following location based on your deployment method:

| Deployment | File Path |
| --- | --- |
| Windows | <MD Core installation folder>\external_allowlist.json |
| Linux VM/Physical | /etc/ometascan/external_allowlist.json |
| Docker | /opt/ometascan/core_data/external_allowlist.json |

Info
> **Note for Docker users**: The file is located in the `CORE_DATA_PATH` directory, which can be modified using environment variables.

### [File Format](/docs/mdcore/v5.22.1/configuration/hardening-for-external-scanners-and-post-actions#file-format)

The file should contain a JSON array of strings, with each string representing an allowed command:

jsonCopy[
"/usr/bin/clamscan",
"/opt/scripts/custom_scanner.sh",
"python3 /path/to/script.py",
"C:\\Program Files\\CustomScanner\\scan.exe",
"/usr/local/bin/sanitize.sh"
]
### [Configuration Rules](/docs/mdcore/v5.22.1/configuration/hardening-for-external-scanners-and-post-actions#configuration-rules)

1. Each entry must be a complete command string (including parameters if needed)
2. Include the full path to the executable
3. For Windows paths, use double backslashes () in your JSON
4. Commands are case-sensitive
5. Duplicate or empty entries will be skipped

### [File permissions](/docs/mdcore/v5.22.1/configuration/hardening-for-external-scanners-and-post-actions#file-permissions)

When the configuration has been done. Admin should change the permission of the file external_allowlist.json

#### [Linux](/docs/mdcore/v5.22.1/configuration/hardening-for-external-scanners-and-post-actions#linux)

ShellCopysudo chmod 400 /path/to/file/external_allowlist.json
sudo chown metascan:metascan /path/to/file/external_allowlist.json
#### [Windows](/docs/mdcore/v5.22.1/configuration/hardening-for-external-scanners-and-post-actions#windows)

We should only allow read for Admin and SYSTEM account

## [Enabling the Feature](/docs/mdcore/v5.22.1/configuration/hardening-for-external-scanners-and-post-actions#enabling-the-feature)

The feature is automatically enabled when the `external_allowlist.json` file exists:

- If the content of external_allowlist.json is in right format -> allow the commands in the file
- If the content of external_allowlist.json is in wrong format or empty -> it means that **zero** commands has been configured -> MetaDefender Core's admin users cannot set any command to either external scanner nor Post-Actions

## [Using the Web Interface](/docs/mdcore/v5.22.1/configuration/hardening-for-external-scanners-and-post-actions#using-the-web-interface)

After configuring the allowlist:

1. External Scanner and Post Action configuration screens will display a combo box with allowlisted commands
2. Commands that are not on the allowlist will be marked with a warning icon
3. When editing non-compliant configurations, warning messages will appear:

   - For Post Actions: "Your action does not comply with security rules. Please choose an action from the approved list."
   - For External Scanners: "Your scanner does not comply with security rules. Please choose a scanner from the approved list."
