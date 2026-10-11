<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-getting-a--user-is-not-allowed-to-log-in--error-when-mu -->

# Why am I getting a "User is not allowed to log in" error when multiple domains are added to workflow for authentication?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Notes:

- This article applies to newer versions on MetaDefender Kiosk that support multiple domain authentication.
- This article applies for workflow login methods using Active Directory

Issues related to “User is not allowed to log in” can arise from:

1. Users are not setup as allowed members in the workflow configuration “Properties & Membership” section.
2. Groups are not setup as allowed in the workflow configuration “Properties & Membership” section.
3. AD User account is not part of any groups that are allowed in “Properties & Membership” section.
4. Same username exists on different Active Directories.

To resolve these issues:

1. Make sure that the correct user account and groups are allowed in the “Properties & Membership” section.
2. Check that the AD user account is part of the correct AD group allowed in “Properties & Membership” section.
3. For user account that share the same username across different domains, please ensure the above and also, make sure to use the following username format at the login prompt: `DOMAIN\username`. In particular, this may be the root cause of most integration with multiple domains. MetaDefender Kiosk will need to know which Directory to query for the expected `username` to avoid unexpected behavior or conflict in case the same username is configured differently on each domain.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/support).
