<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/why-does-mft-to-mft-fails-after-upgrade- -->

# Why does MFT to MFT fails after upgrade?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article applies to all MetaDefender Managed File Transfer releases deployed on Windows systems.

If your MFT to MFT integration doesn’t work after the MFT upgrade from version 3.6.2 and lower to a version 3.6.3 or newer, please check the details below:

MFT to MFT uses an API call method of communication, which starting with MFT version 3.6.3 requires a new header called Group_ID. Since this is not configured, the API call will fail.

This situation can be resolved by enabling an option in MFT called: “Allow Users to Upload Files Without Specifying Group Membership”.

To enable this option, please navigate to the MFT UI -> Settings -> Global Settings -> Files -> enable the option Allow Users to Upload Files Without Specifying Group Membership -> Click on Update.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support).
