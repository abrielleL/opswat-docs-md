<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/using-restart-action-of-installmissingpatches-when-update-macos -->

# Using input.restart_action with InstallMissingPatches on macOS Software Update

This article is applied to MetaDefender Endpoint Security SDK (OESIS) from version **4.3.4105.0** and later releases deployed on MacOS systems.

## [**Problem**](/docs/mdsdk/knowledge-base/using-restart-action-of-installmissingpatches-when-update-macos#problem)

The `InstallMissingPatches` method in MetaDefender Endpoint Security SDK’s Software Update module on macOS initiates the patch installation process and may automatically trigger a system restart without user confirmation.

This behavior occurs because our SDK relies on macOS’s native update mechanism, which determines whether a restart is required based on the type of patch being applied. As a result, the system may reboot automatically for certain updates, depending on macOS’s default behavior.

## [**Solution**](/docs/mdsdk/knowledge-base/using-restart-action-of-installmissingpatches-when-update-macos#solution)

Starting with SDK build version **4.3.4105.0**, we introduced a new input flag for `InstallMissingPatches` to control the restart behavior of macOS:

- **Field Name:** `input.restart_action`
- **Field Type:** `number`
- **Description:** Specifies the system restart behavior during macOS patch installation.
- **Behavior:**

  - If `restart_action` is **omitted** or the value is **0** (default behavior):

    - The update will be downloaded and macOS will restart automatically to install the patches (if required).
    - The system may restart multiple times during the update process.
  - If `restart_action` is set to **1**:

    - The update will be downloaded but will not trigger an automatic restart.
    - The system will wait for the user to manually initiate the restart via the Software Update UI.

### [Usage Example](/docs/mdsdk/knowledge-base/using-restart-action-of-installmissingpatches-when-update-macos#usage-example)

WITHOUT restartWITH automatic restartCopy{
"input": {
"signature": 100192,
"method": 1014,
"restart_action": 1,
"patches": [
{
"title": "macOS Sequoia 15.4-24E248",
"product": "macOS Sequoia",
"vendor": "Apple Inc."
}
]
}
}{
"input": {
"signature": 100192,
"method": 1014,
"patches": [
{
"title": "macOS Sequoia 15.4-24E248",
"product": "macOS Sequoia",
"vendor": "Apple Inc."
}
]
}
}
## [Why is the applied patch still shown in GetMissingPatches?](/docs/mdsdk/knowledge-base/using-restart-action-of-installmissingpatches-when-update-macos#why-is-the-applied-patch-still-shown-in-getmissingpatches)

If the system isn't restarted after applying a patch, **the patch may still appear** in `GetMissingPatches`, as certain updates require a reboot to complete. Others may install fully without restarting and won’t reappear.

To complete installation for patches that need a reboot, you can restart macOS using one of two methods:

### [Option 1: Invoke InstallMissingPatches without `restart_action`](/docs/mdsdk/knowledge-base/using-restart-action-of-installmissingpatches-when-update-macos#option-1-invoke-installmissingpatches-without-restart_action)

Invoke `InstallMissingPatches` without `input.restart_action` parameter, or with `input.restart_action = 0`. It will restart immediately to install the macOS update.

### [Option 2: Manually restart to install the macOS update](/docs/mdsdk/knowledge-base/using-restart-action-of-installmissingpatches-when-update-macos#option-2-manually-restart-to-install-the-macos-update)

Open **Settings → Software Update →** select the missing patch, then click the **Restart Now** button.

Support

If **further assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
