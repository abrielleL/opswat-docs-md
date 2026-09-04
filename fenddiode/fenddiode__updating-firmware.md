<!-- source: https://www.opswat.com/docs/fenddiode/updating-firmware -->

# Updating Firmware

This section contains instructions for updating firmware on a Fend Diode.

To update your data diode’s firmware, download the latest firmware for your diode from <https://my.opswat.com/>. For instructions on getting firmware from MyOPSWAT please see the section on [Firmware & Software Downloads](https://www.opswat.com/docs/fenddiode/firmware-software-downloads). If you have issues logging in or downloading support material, contact us at [fendsupport@opswat.com](mailto:fendsupport@opswat.com).

**Before updating your diode please note:**

1. **You can only upgrade to a version of firmware that is** ***newer*** **than the version on your diode (cannot downgrade) and you can only upgrade to a version that is compatible with your hardware.** To determine the model and firmware version of your current diode, log into your diode via the web browser configuration interface and go to “About” in the “System” section. For details see [**Fend Data Diode Model Numbers**](https://www.opswat.com/docs/fenddiode/introduction/connections-and-interface#fend-data-diode-model-numbers) and [**General/System Settings**](https://www.opswat.com/docs/fenddiode/configuration-settings/system-settings).
2. **You must be** ***physically*** **present when the diode is updating in order to confirm that the update was successful using the diode LED lights. If the update is not confirmed within 5 minutes of completion, it will be canceled, and the diode will revert back to the original firmware.** The firmware update process should take around 1 minute to complete.

## [Firmware Update Path](/docs/fenddiode/updating-firmware#firmware-update-path)

Before updating your diode, be sure that you are following the correct firmware upgrade path. Some firmware versions can only be upgraded to other specific firmware versions before upgrading further. Use the following table as a guide.

| Current Firmware Version | Required Upgrade Step |
| --- | --- |
| Pre-4.0.3 | 4.0.3 |
| 4.0.3-4.2.0 | 4.2.1 |
| 4.2.1 | 4.2.7 |
| 4.2.7+ | Latest Firmware Version |

To start the update process, log into the diode’s configuration interface via your web browser. The firmware update feature can be found in the “System” section, under “Firmware Update”:

To upload a new firmware file, press the “Browse” folder icon and a file-selection window will appear. Navigate to the provided firmware file then click “Open”.

When the appropriate file has been selected, press the “Update” icon to begin the update.

When the firmware update process begins, a window will appear displaying that a firmware update is in progress.

Once both sides of the diode are finished updating, the completion screen will be displayed. It will ask you to ensure that both sides of the diode are flashing the indicated LED pattern to confirm the update was a success.

- Firmware Update Success – The red, yellow, and green LED's in Banks A and C should be fast blinking
- Firmware Update Fail – If only the red light in either Banks A or C is flashing, the firmware update has failed.

You **must** confirm a successful update by selecting “Yes” for the firmware update to complete. If LED's are not displaying the indicated pattern, select “No” and the process will be aborted. After 5 minutes, if you fail to respond to the confirmation window, the update is canceled and the diode will revert to the original firmware.

**After the firmware update is complete,** **make sure to reconnect to the diode and review all diode settings to confirm any new settings.**
