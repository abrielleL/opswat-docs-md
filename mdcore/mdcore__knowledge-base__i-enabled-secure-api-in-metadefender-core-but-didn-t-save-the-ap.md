<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/i-enabled-secure-api-in-metadefender-core-but-didn-t-save-the-ap -->

# I enabled Secure API in MetaDefender Core but didn't save the API key. How do I reset it?

**Check Your Version:** This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

## [**Summary:**](/docs/mdcore/knowledge-base/i-enabled-secure-api-in-metadefender-core-but-didn-t-save-the-ap#summary)

When you enable the Secure API setting, MetaDefender Core displays the API key once and warns that it cannot be retrieved again. That warning is accurate but narrow: you cannot recover the exact value that was shown, but you are not locked out.

The API key is bound to a user account, so you can simply generate a new key for that user. Generating a new key replaces the old one, and the lost value becomes irrelevant.

## [Resolution](/docs/mdcore/knowledge-base/i-enabled-secure-api-in-metadefender-core-but-didn-t-save-the-ap#resolution)

To generate a new API key:

1. Open the MetaDefender Core console and go to User Management > Users and Groups.
2. Select the user account you wish to manage the API key for.
3. In the API key section click Generate.
4. Click Save changes for the new key to take effect.
5. Copy the new key and store it somewhere safe before leaving the page.

The Edit User dialog in MetaDefender Core. Click Generate next to the API key field to create a new key, then click Save changes. Be sure to copy the new key before closing

The previous key is invalidated as soon as the new one is saved, so any integration still using the old value will need to be updated with the new key.

**Support:**

If you have questions, concerns or issues regarding **MetaDefender** **Core**, please open a [Support Case](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).
