<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/why-my-kiosk-integration-stopped-working-after-mft-upgrade- -->

# Why my KIOSK integration stopped working after MFT upgrade?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article applies to all MetaDefender Managed File Transfer releases deployed on Windows systems.

If your Kiosk integration doesn’t work after the MFT upgrade from version 3.6.2 and lower, to a version 3.6.3 or newer, or it will assign the uploaded files to a Guest account instead of the mentioned user account, please check the details below:

Kiosk uses an API call method of communication, which starting with MFT version 3.6.3 requires a new header called Group_ID. Since this is not configured, the API call will fail.

This situation can be resolved by enabling an option in MFT called: “Allow Users to Upload Files Without Specifying Group Membership”.

To enable this option, please navigate to the MFT UI -> Settings -> Global Settings -> Files -> enable the option Allow Users to Upload Files Without Specifying Group Membership -> Click on Update.

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support).
