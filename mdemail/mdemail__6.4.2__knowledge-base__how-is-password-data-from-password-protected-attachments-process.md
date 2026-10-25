<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/knowledge-base/how-is-password-data-from-password-protected-attachments-process -->

# How is password data from password-protected attachments processed by MetaDefender Email Gateway Security?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Email Gateway Security V4 and V5 releases deployed on Windows Systems.

The passwords for password-protected email attachments are sent to MetaDefender Core via a header, so provided the connection between MetaDefender Email Gateway Security and MetaDefender Core is secured with HTTPS, this should be sufficient.

These passwords are only temporarily stored in memory by MetaDefender Email Gateway Security.

These passwords are never stored permanently, in any folder or in any database on the MetaDefender Email Gateway Security or MetaDefender Core side.

Once the email process workflow is completed, which is usually within a few seconds, the password is permanently deleted from memory.

Support:

For further queries, concerns or issues regarding **How MetaDefender Email Gateway Security Processes Password Protected Attachments**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
