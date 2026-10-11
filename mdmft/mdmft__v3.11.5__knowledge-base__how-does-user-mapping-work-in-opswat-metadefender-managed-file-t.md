<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t -->

# How does User Mapping work in OPSWAT MetaDefender Managed File Transfer?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [**Overview**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#overview)

User Mapping allows MetaDefender Managed File Transfer (MFT) to associate an alternate identity with an existing MFT user. A single MFT account can therefore be recognized through different identity representations, such as a local username, Active Directory account, external or SSO identity, guest identifier, or third-party identifier.

User Mapping is useful when an authentication or transfer-ownership request identifies a person differently from the identity stored on that person's primary MFT account.

**Key concept:** A mapping belongs to one primary MFT user. The mapped value is an alternate identity for that user; it is not a two-way link between two independent accounts.

## [**What User Mapping does**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#what-user-mapping-does)

A User Mapping defines an additional identity through which an existing MFT user can be recognized. For example, an MFT user named JohnAD could have an alternate local identity named Johnlocal. When a supported workflow presents Johnlocal, MFT can resolve it to the primary JohnAD account.

The alternate identity does not need to exist as a separate MFT user. During identity resolution, MFT first checks for a directly matching user and then checks the configured User Mappings.

## [**Supported identity types**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#supported-identity-types)

| **Identity type** | **Identity information** |
| --- | --- |
| Local user | Username or email address |
| Active Directory user | Username and domain |
| External or SSO user | Username or email address |
| Guest user | Guest PIN code |
| Third-party identity | Third-party identifier |

## [**Common examples**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#common-examples)

### [**Local identity mapped to an Active Directory user**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#local-identity-mapped-to-an-active-directory-user)

An organization may have an Active Directory user named JohnAD who must also be recognized by the local identity Johnlocal. In this example, JohnAD is the primary MFT user and Johnlocal is an alternate identity owned by that user.

| **Primary MFT user** | **Alternate identity type** | **Alternate identity** |
| --- | --- | --- |
| JohnAD | Local | Johnlocal |

### [**Active Directory identity in another domain**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#active-directory-identity-in-another-domain)

A user may have a different username in another Active Directory domain. An Active Directory mapping identifies that alternate account by both username and domain.

| **Primary MFT user** | **Mapped AD username** | **Mapped AD domain** |
| --- | --- | --- |
| john.local | JohnAD | DomainB |

### [**External, guest, and third-party identities**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#external-guest-and-third-party-identities)

An external or SSO username or email address can be associated with a primary MFT user. MFT also supports alternate identities based on a guest PIN code or a third-party identifier.

## [**How User Mapping works**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#how-user-mapping-works)

1. An administrator selects the existing MFT user who will own the mapping.

2. The administrator selects the alternate identity type and enters the required identity information.

3. MFT saves the alternate identity under the selected primary user.

4. During a supported request, MFT first checks for a directly matching user.

5. If no direct match is found, MFT checks the configured User Mappings and resolves a matching identity to its primary user.

## [**Information stored in a mapping**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#information-stored-in-a-mapping)

| **Field** | **Description** |
| --- | --- |
| Identity type | The identity system represented by the mapping |
| Primary identity value | A username, guest PIN, or third-party identifier |
| Secondary identity value | An email address or Active Directory domain, when applicable |
| Owning MFT user | The primary MFT user to which the alternate identity resolves |

## [**Potential use case scenarios**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#potential-use-case-scenarios)

### [**1. Migration from local accounts to Active Directory**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#1-migration-from-local-accounts-to-active-directory)

An organization may replace locally managed MFT accounts with Active Directory authentication. The Active Directory account can be the primary MFT user, while the previous local username or email address is retained as an alternate identity.

| Primary MFT user | Alternate type | Alternate identity |
| --- | --- | --- |
| `jsmith@corp.example` | Local | `jsmith` |

Requests using the former local identity can then resolve to the primary Active Directory user. Local mappings accept a username or email address, while Active Directory mappings require a username and domain.

### [**2. Consolidating users from multiple AD domains**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#2-consolidating-users-from-multiple-ad-domains)

After a merger or directory restructuring, one person may have accounts in two Active Directory domains. The account used as the primary MFT user can have the other domain account configured as an alternate identity.

| Primary MFT user | Mapped username | Mapped domain |
| --- | --- | --- |
| `john.smith@newcorp.example` | `jsmith` | `LegacyDomain` |

This allows the legacy domain identity to resolve to the primary user without creating a separate mapping between two independent MFT accounts.

### [**3. Introducing SSO for existing MFT users**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#3-introducing-sso-for-existing-mft-users)

An organization may introduce SAML or OIDC SSO while retaining existing MFT users. If the identity provider supplies a different username or email address, that external identity can be associated with the existing MFT user.

| Primary MFT user | Alternate type | External identity |
| --- | --- | --- |
| `john.smith` | External/SSO | `john.smith@company.example` |

External mappings support either a username or email address.

### [**4. Username or email-address changes**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#4-username-or-email-address-changes)

When a person’s username or email address changes, the previous value can be retained as an alternate local or external identity.

| Primary MFT user | Alternate type | Previous identity |
| --- | --- | --- |
| `jane.lee@company.example` | External/SSO | `jane.wong@company.example` |

This provides another recognized representation of the same primary MFT user.

## [**Managing User Mappings**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#managing-user-mappings)

User Mappings can be managed individually or through bulk import and export. Administrators can manage mappings for any user. Helpdesk administrators can manage mappings for eligible non-administrative users. Regular users cannot manage User Mappings, including their own.

## [**Import and export considerations**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#import-and-export-considerations)

**Important:** Bulk import replaces the complete set of existing User Mappings. Export the current mappings before importing, and make sure the import file contains every mapping that must remain configured.

The bulk operation is transactional: the existing mappings are replaced as one operation. If the import fails, the transaction is rolled back so that a partial configuration is not left behind. Duplicate identity combinations cause the import to fail.

## [**Best practices**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#best-practices)

1. Treat the selected MFT user as the primary owner of every mapping.
2. Choose the identity type that matches the alternate identity being entered.
3. Include both the username and domain for Active Directory mappings.
4. Review mappings when usernames, email addresses, domains, or identity providers change.
5. Do not assign the same alternate identity to more than one primary user.
6. Export the current mappings before performing a bulk import.
7. Validate the complete import file before applying it in production.

## [**Summary**](/docs/mdmft/v3.11.5/knowledge-base/how-does-user-mapping-work-in-opswat-metadefender-managed-file-t#summary)

User Mapping enables MetaDefender MFT to associate alternate local, Active Directory, external, guest, or third-party identities with one primary MFT user. It supports identity resolution when an incoming identity differs from the user's primary MFT identity.

For reliable results, keep each mapping directional, use the correct identity type, and protect the existing configuration by exporting it before bulk changes.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
