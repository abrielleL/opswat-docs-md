<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/why-does----guestidentifier----fail-to-dynamically-populate-the- -->

# Why Does [%]GuestIdentifier[%] Fail to Dynamically Populate the Unique Identifier in the Guest Welcome Email?

Summarize Page    Connect to Cursor Connect to VS Code

In MetaDefender Managed File Transfer version 3.8.1 and 3.8.2, the placeholder [%]GuestIdentifier[%] does not dynamically populate with the unique identifier in the guest welcome email. Instead, the placeholder remains unchanged as [%]GuestIdentifier[%], preventing the correct guest identifier from being displayed.

This issue is caused by a known bug in MetaDefender Managed File Transfer version 3.8.1 and 3.8.2 that prevents the `[%]GuestIdentifier[%]` placeholder from being replaced with the correct value in guest emails.

This issue has been resolved in MetaDefender Managed File Transfer version 3.9.0. Upgrading to this version or a later release will restore the expected functionality.

Please refer to this article for how to upgrade MetaDefender Managed File Transfer: [Upgrading MetaDefender Managed File Transfer](/docs/mdmft/installation/updating-and-upgrading).

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support).
