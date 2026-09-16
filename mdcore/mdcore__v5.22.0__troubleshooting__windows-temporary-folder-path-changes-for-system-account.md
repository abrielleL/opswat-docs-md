<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/troubleshooting/windows-temporary-folder-path-changes-for-system-account -->

# Windows Temporary Folder Path Changes for SYSTEM Account

## [Overview](/docs/mdcore/v5.22.0/troubleshooting/windows-temporary-folder-path-changes-for-system-account#overview)

Microsoft has recently (Feb 2026) introduced security improvements that change the default temporary folder location for services and applications running under the **SYSTEM** account.

This is a Windows operating system change and is not related to any changes in MetaDefender Core product.

## [What Changed?](/docs/mdcore/v5.22.0/troubleshooting/windows-temporary-folder-path-changes-for-system-account#what-changed)

Microsoft introduced a new secure temporary folder location called `C:\Windows\SystemTemp` specifically for processes running as the SYSTEM account. This folder has stricter security permissions to prevent path redirection attacks.

### [Previous Behavior](/docs/mdcore/v5.22.0/troubleshooting/windows-temporary-folder-path-changes-for-system-account#previous-behavior)

- SYSTEM account temp folder: `C:\Windows\Temp`

### [New Behavior](/docs/mdcore/v5.22.0/troubleshooting/windows-temporary-folder-path-changes-for-system-account#new-behavior)

- SYSTEM account temp folder: `C:\Windows\SystemTemp`

**Note:** This change only affects applications running as the **SYSTEM** account. Applications running under user accounts are not affected and will continue to use their existing temp folder locations.

### [What You Might Observe](/docs/mdcore/v5.22.0/troubleshooting/windows-temporary-folder-path-changes-for-system-account#what-you-might-observe)

If your environment is affected, you may notice:

- Temporary files being created in `C:\Windows\SystemTemp` instead of `C:\Windows\Temp` .
- Applications that hardcode the path to `C:\Windows\Temp` may not find expected temporary files.
- Increased disk usage in the `C:\Windows\SystemTemp` directory.

For example, the temporary folder for NGINX now will be in `C:\Windows\SystemTemp\ometascan\`

## [Impact on MetaDefender Core](/docs/mdcore/v5.22.0/troubleshooting/windows-temporary-folder-path-changes-for-system-account#impact-on-metadefender-core)

Currently, there is no known impact on MetaDefender Core services. However, if you experience any issues related to this Windows change, please contact OPSWAT Support for assistance.
