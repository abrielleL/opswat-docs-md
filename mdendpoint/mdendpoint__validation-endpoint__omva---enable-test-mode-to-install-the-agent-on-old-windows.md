<!-- source: https://www.opswat.com/docs/mdendpoint/validation-endpoint/omva---enable-test-mode-to-install-the-agent-on-old-windows -->

# OMVA - Install and operate OMVA on Windows 7 SP1 without SHA2

## Overview

This document provides instructions for enabling **"test-mode"** on older Windows operating systems to facilitate the installation and operation of the OPSWAT Media Validation Agent (OMVA). Test mode allows the installation of unsigned drivers and software, which may be necessary for compatibility with legacy systems.

## Prerequisites

- Administrative access to the Windows machine.
- Command Prompt with elevated privileges (Run as Administrator).
- Prepare the OMVA installer with a version larger than or equal to 2.0.12.302

## Enabling Test Mode

###   Follow these steps to enable test mode on your Windows system:

- **Step 1:** Download the [**EnableTestModeAndReboot.bat**](https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/EnableTestModeAndReboot.bat) to the target machine.
- **Step 2**:
  - Option 1: Right-click on the script and select **Run as administrator** option.
  - Option 2:
    - Click on the **Start** menu.
    - Type `cmd` in the search bar.
    - Right-click on **Command Prompt** and select **Run as administrator**.
    - Redirect the location path to the folder including the script file (Ex: `cd /d <folder_path>`).
    - Run the command:`.\EnableTestModeAndReboot.bat`
- **Step 3:** The script will restart the machine, and you will see the "Test Mode" watermark in the bottom right corner (see the sample image attached below).

![](https://uploads.developerhub.io/prod/2x2P/bo0fooa55omk7awopd3vanf9gfp7mu1uqqax2p581htzq158hxsw2atisdagox0r.png)

## Installing the OMVA

Once test mode is enabled, proceed with the installation of the OMVA as normal.

Detailed instructions can be found [here](https://www.opswat.com/docs/mdkiosk/v4.7.2/operating/opswat-media-validation-agent#installing-the-agent)

Verification

After installation, verify that the OMVA is functioning correctly:

1. Open the application or service associated with the OMVA.
2. Check for any error messages or issues during startup.
3. Confirm that the agent is operating as expected.

## Troubleshooting

If you encounter problems during the installation of the OMVA, please go to the folder: `%PROGRAMDATA%\OPSWAT\OPSWAT-OMVA` and collect all files to send to us for investigation.

## Conclusion

Enabling test mode allows the installation of the OMVA on older Windows systems that may not support signed drivers. Thus, following the steps outlined in this document can ensure a smooth installation process.

## Disable test mode

To disable test mode and revert to standard mode, simply run the [**DisableTestModeAndReboot.bat**](https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/DisableTestModeAndReboot.bat) script using the same steps as when enabling it.

## Notes

- Enabling test mode can be useful for installing certain applications or drivers on older Windows systems. However, when test mode is active, please ensure that you only install applications from trusted sources, as this mode bypasses standard certificate verification.
