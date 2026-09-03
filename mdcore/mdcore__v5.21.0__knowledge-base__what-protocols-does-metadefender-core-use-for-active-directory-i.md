<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/what-protocols-does-metadefender-core-use-for-active-directory-i -->

# What Protocols Does MetaDefender Core Use for Active Directory Integration?

This article applies to all MetaDefender Core releases deployed on Windows/Linux systems.

> ## [Overview](/docs/mdcore/v5.21.0/knowledge-base/what-protocols-does-metadefender-core-use-for-active-directory-i#overview)
>
> Metadefender Core integrates with Microsoft Active Directory (AD) using Lightweight Directory Access Protocol (LDAP). Unlike other authentication protocols such as Kerberos or NTLM, this application relies solely on LDAP/LDAPS for directory services and user authentication.
>
> ## [Protocols Not Used](/docs/mdcore/v5.21.0/knowledge-base/what-protocols-does-metadefender-core-use-for-active-directory-i#protocols-not-used)
>
> ### [Kerberos:](/docs/mdcore/v5.21.0/knowledge-base/what-protocols-does-metadefender-core-use-for-active-directory-i#kerberos)
>
> - Not used for authentication or Single Sign-On (SSO).
> - No Kerberos ticket requests are generated.

### [NTLM:](/docs/mdcore/v5.21.0/knowledge-base/what-protocols-does-metadefender-core-use-for-active-directory-i#ntlm)

- Not supported.
- The application does not rely on NTLM hashes for authentication.

## [Steps to Configure](/docs/mdcore/v5.21.0/knowledge-base/what-protocols-does-metadefender-core-use-for-active-directory-i#steps-to-configure)

Refer to the official documentation for detailed configuration steps: [User directories](/docs/mdcore/v5.21.0/configuration/user-directories)

## [Verify the Change](/docs/mdcore/v5.21.0/knowledge-base/what-protocols-does-metadefender-core-use-for-active-directory-i#verify-the-change)

Refer to the official documentation for verification steps: [User directories](/docs/mdcore/v5.21.0/configuration/user-directories)

## [Troubleshooting](/docs/mdcore/v5.21.0/knowledge-base/what-protocols-does-metadefender-core-use-for-active-directory-i#troubleshooting)

If you have queries, concerns, or issues regarding Metadefender Core AD integration methods, please open a Support Case with the OPSWAT team via phone, online chat, or form, or feel free to ask the community on our OPSWAT Expert Forum.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
