<!-- source: https://www.opswat.com/docs/filescan/faq/how-to-update-yara-rules-in-an-air-gapped-offline-environment -->

# How to update YARA rules in an air-gapped/offline environment?

To update the YARA rule set in an air-gapped/offline sandbox environment, please follow these steps:

- Search for the **latest release** in the fsYara GitHub repository: <https://github.com/filescanio/fsYara/releases>
- Click on that release, and download the `master_file.yarc` file from the **release assets**:

- Transfer the downloaded `master_file.yarc` to your offline environment (e.g. using a USB drive)
- Replace the current master file in `/home/sandbox/sandbox/transform/yara/rules/master_file.yarc` with the new master file, and ensure that the `sandbox` user owns the new file:

BashCopycd /PATH/TO/YOUR/USB-DRIVE
sudo cp -f master_file.yarc /home/sandbox/sandbox/transform/yara/rules/master_file.yarc
sudo chown sandbox:sandbox /home/sandbox/sandbox/transform/yara/rules/master_file.yarc

- Restart the `transform` component of the `sandbox` service, so the updated YARA rules are loaded into memory:

BashCopysudo service sandbox restart-transform

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
