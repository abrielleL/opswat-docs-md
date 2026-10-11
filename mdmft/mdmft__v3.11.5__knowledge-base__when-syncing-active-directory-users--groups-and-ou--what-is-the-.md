<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/when-syncing-active-directory-users--groups-and-ou--what-is-the- -->

# When syncing Active Directory users, groups and OU, what is the rule order that takes precedence?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

When MetaDefender Managed File Transfer (MFT) synchronizes users from Active Directory or LDAP, include and exclude filters can be applied at the organizational unit (OU), group, and individual-user levels. This article explains which rule takes precedence when those filters overlap, and what result to expect when MFT evaluates conflicting scope definitions.

The key rule is simple: **individual-user rules take highest precedence, group rules take second precedence, and OU rules take lowest precedence**. In practice, an explicit user rule overrides a group rule, and a group rule overrides an OU rule.

## [**At a glance**](/docs/mdmft/v3.11.5/knowledge-base/when-syncing-active-directory-users--groups-and-ou--what-is-the-#at-a-glance)

| Priority | Filter level | Effect |
| --- | --- | --- |
| 1 — highest | Individual user | Overrides group and OU rules for that specific account. |
| 2 | Group | Overrides OU-based scope for members affected by that group rule. |
| 3 — lowest | Organizational unit | Defines the broad directory scope unless a more specific rule changes the result. |

MFT also has a separate administrative mapping path in some deployments. Because of that, administrator accounts may still synchronize even when standard-user filters remove similar accounts from the normal sync scope.

The same directory object cannot be placed in both the Include and Exclude lists in the user interface.

## [**How MFT evaluates overlapping rules**](/docs/mdmft/v3.11.5/knowledge-base/when-syncing-active-directory-users--groups-and-ou--what-is-the-#how-mft-evaluates-overlapping-rules)

A reliable way to understand the outcome is to separate **user selection** from **group metadata**. MFT may synchronize group objects needed to represent membership for users that are already in scope, even when those group objects do not expand the selected user list.

| Stage | Question MFT resolves | Practical effect |
| --- | --- | --- |
| 1. OU scope | Which parts of the directory are broadly eligible? | Included and excluded OUs establish the baseline scope. |
| 2. Group overrides | Do group rules add or remove members from that baseline? | Group rules take precedence over OU rules. |
| 3. User overrides | Is a specific user explicitly included or excluded? | The individual-user rule is decisive for that account. |
| 4. Membership metadata | Which group objects are needed for selected users? | Related groups can appear without expanding the selected user population. |

## [**What this means in practice**](/docs/mdmft/v3.11.5/knowledge-base/when-syncing-active-directory-users--groups-and-ou--what-is-the-#what-this-means-in-practice)

- **Including one user** synchronizes that user and will also synchronize the group objects tied to that user's memberships.
- **Including one user does not automatically synchronize every other member** of those groups.
- **Including one group** synchronizes the eligible users in that group based on the active scope rules.
- **Related group objects do not usually expand user scope** by themselves.
- **Nested groups can behave differently** because MFT can traverse the nested structure and synchronize nested groups and users, including across OU boundaries.

> If User 1 belongs to Groups 1 through 5 and only User 1 is explicitly included, the result can contain User 1 plus Groups 1 through 5. Users 2 through 5 do not synchronize simply because they share those group memberships.

## [**Common precedence outcomes**](/docs/mdmft/v3.11.5/knowledge-base/when-syncing-active-directory-users--groups-and-ou--what-is-the-#common-precedence-outcomes)

| Configuration | Observed result | Rule demonstrated |
| --- | --- | --- |
| Include User 1; exclude Group 1 | User 1 still synchronizes. | Explicit user include overrides group exclusion. |
| Include Group 1; exclude User 3 | User 3 does not synchronize. | Explicit user exclusion overrides group inclusion. |
| Exclude an OU; include a group inside it | The included group and eligible members synchronize. | Group inclusion overrides OU exclusion. |
| Include an OU; exclude a group inside it | Members affected by the excluded group are removed. | Group exclusion overrides OU inclusion. |
| Include Group 1; exclude overlapping Group 4 | Users that are only affected by the excluded overlap are removed unless explicitly included. | For overlapping group rules, exclusion wins unless an individual user rule overrides it. |

An explicit user include can cause related group objects to appear even when one of those groups is excluded. This does **not** mean the excluded group's other users were included. It only means MFT retained the selected user's membership context.

## [**What to expect when synchronizing?**](/docs/mdmft/v3.11.5/knowledge-base/when-syncing-active-directory-users--groups-and-ou--what-is-the-#what-to-expect-when-synchronizing)

- An Include entry is not always an exclusive allowlist. A broader OU or default scope may still bring in additional users unless it is also narrowed.
- Extra groups can be normal. MFT may synchronize them to preserve membership information for users already in scope.
- Extra users are not normally expected just because related group objects appear.
- Empty groups may disappear if filtering removes all synchronized members from those groups.
- Administrator accounts may follow separate synchronization logic from standard users.
- After a failed synchronization, MFT may continue to reflect the last successful directory state until a later sync finishes successfully.

If you want to synchronize only one specific group, first remove or exclude the broader OU scope that would otherwise keep additional users eligible. Then include only the target group and review the preview carefully.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
