<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/configuration/settings---managed-file-transfer -->

# Settings → Managed File Transfer

MetaDefender Managed File Transfer (formerly MD Vault) is a secure solution to transfer your sensitive data across your critical infrastructure networks. You can set up an integration between MetaDefender Drive and MetaDefender Managed File Transfer to securely transfer and store the safe files after a completed scan by MetaDefender Drive.

Info

Before you start, you need to deploy a MetaDefender Managed File Transfer instance for your organization using the following [MetaDefender Managed File Transfer Installation Instructions](https://docs.opswat.com/mdmft).

## [Setting Up Managed File Transfer Integration](/docs/mddrive/v4.4.2a/configuration/settings---managed-file-transfer#setting-up-managed-file-transfer-integration)

1. Go to Settings → MetaDefender MFT. The MetaDefender MFT page will show if there are any MetaDefender Managed File Transfer instances connected to the currently plugged drive.

2. Click Add MFT Instance, and enter the MFT URL and API Key in the Add a New MetaDefender MFT instance window, then press Add MFT.

Info

One MetaDefender Drive can connect to multiple instances of MetaDefender Managed File Transfer.

3. After a successful connection, you can toggle the **Transfer as Guest** option to **NO**, and you will be able to transfer files as administrator and set the expiration time. By default, MetaDefender Drive transfers data to newly connected Managed File Transfer instances as a **Guest**.

If you transfer the clean data as a **Guest**, your data will be securely stored for a specified amount of time and cleared afterward. The provided **Guest ID** can be used to log in to MetaDefender Managed File Transfer and retrieve your files.

..
