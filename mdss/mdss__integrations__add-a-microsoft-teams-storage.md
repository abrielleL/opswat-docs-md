<!-- source: https://www.opswat.com/docs/mdss/integrations/add-a-microsoft-teams-storage -->

# Add a Microsoft Teams Storage

MetaDefender Storage Security supports scanning files shared through **Microsoft Teams** by integrating with the underlying Microsoft storage services used by Teams: **OneDrive** and **SharePoint**.

## [How Teams Stores Files](/docs/mdss/integrations/add-a-microsoft-teams-storage#how-teams-stores-files)

### [Teams Chat (1:1 and Group Chats → OneDrive)](/docs/mdss/integrations/add-a-microsoft-teams-storage#teams-chat-11-and-group-chats--onedrive)

When a user sends a file in a Teams chat, the file is uploaded to the sender’s OneDrive

These files are stored in a folder named **Microsoft Teams Chat Files**

- Only files sent by that user appear in their OneDrive folder
- Other chat participants see read-only references to the file, but the actual file remains in the sender’s OneDrive

### [Teams Channels (Channels → SharePoint)](/docs/mdss/integrations/add-a-microsoft-teams-storage#teams-channels-channels--sharepoint)

- Files sent in a Teams channel are stored in the team’s SharePoint site
- They appear under the Documents library, inside a folder named after the channel

## [Integrating OneDrive](/docs/mdss/integrations/add-a-microsoft-teams-storage#integrating-onedrive)

In order to add a OneDrive storage in MetaDefender Storage Security, follow [the documentation](/docs/mdss/integrations/add-an-onedrive-storage).

### [Recommended Configuration for Teams Chat](/docs/mdss/integrations/add-a-microsoft-teams-storage#recommended-configuration-for-teams-chat)

For scanning files sent in Teams chats, we recommend adding the user and the folder location **Microsoft Teams Chat Files.**

This configuration ensures that only files sent by that user in Teams chats are scanned.

## [Integrating SharePoint](/docs/mdss/integrations/add-a-microsoft-teams-storage#integrating-sharepoint)

In order to add a **SharePoint** storage in MetaDefender Storage Security, follow [the documentation](/docs/mdss/integrations/add-a-sharepoint-storage).

### [Recommended Configuration for Teams Channels](/docs/mdss/integrations/add-a-microsoft-teams-storage#recommended-configuration-for-teams-channels)

For scanning files shared in Teams channels, we recommend integrating with the **channel folder** inside the SharePoint site’s *Documents* library

This configuration ensures that only files shared in the selected Teams channel are scanned.

## [Scanning with Deep CDR](/docs/mdss/integrations/add-a-microsoft-teams-storage#scanning-with-deep-cdr)

When using Deep CDR, the sanitized file will not be accessible in Teams by default.

To ensure Teams users can access the sanitized file, you must enable the **“Replace Original File”** feature, following [the documentation](/docs/mdss/configuration/deep-content-disarm-and-reconstruction--deep-cdr-#replace-original-files-with-sanitized-versions).

This replaces the original Teams file with the sanitized version, meaning Teams users will always access the sanitized file in their chat or channel.
