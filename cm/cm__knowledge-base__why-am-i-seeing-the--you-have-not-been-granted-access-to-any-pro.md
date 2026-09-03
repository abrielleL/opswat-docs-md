<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-am-i-seeing-the--you-have-not-been-granted-access-to-any-pro -->

# Why am I seeing the "You have not been granted access to any protected applications in undefined" error when using special characters in Azure group names?

> **Check Your Version:**
>
> This article is applied to MetaDefender Endpoint releases deployed on Windows, Mac and Linux systems.

**Issue:**

Users attempting to log into MetaDefender SDP using Single Sign-On (SSO) may encounter the following error: *"You have not been granted access to any protected applications in* ***undefined****__. Contact your administrator to gain access to applications."*

![](https://uploads.developerhub.io/prod/97qW/fz2woigunqmvfar8y34yfy6m8vv8ze9c6gi2t1ogvknxhw2rk7pk9g6kspf5w6wm.png)

**Cause:**

This issue occurs when the group name in Microsoft Azure does not exactly match the group name configured in My OPSWAT Central Management under **IdP Mapping**. Even minor differences, such as unsupported special characters, can cause the mapping to fail.

**For example:**

Azure Group Name: `ABC & OPSWAT METADEFENDER ENDPOINT`

My OPSWAT Central Management >  IdP Mapping > External IdP Group Name: `ABC OPSWAT METADEFENDER ENDPOINT`

In the above case, the presence of the ampersand & character in Azure but not in My OPSWAT Central Management causes the mismatch, resulting in the access error.

> **Please note:**
>
> The **External IdP Group** field in My OPSWAT Central Management only accepts the following characters: `0-9, A-Z, a-z, _ (underscore), and - (dash)`. Special characters such as `&` are **not allowed** and will result in validation errors.

**Resolution:**

Ensure that the **group name in Azure matches exactly** with the one configured in **My OPSWAT Central Management > IdP Mappings > Group Settings**, and only includes allowed characters.

![](https://uploads.developerhub.io/prod/97qW/nbxgo0jg8hp8ycugbv36b62ko75d62vclzbzquq8hv8v9ncygymlol83tl19vty8.png)

Once the group name in Azure matched the one defined in My OPSWAT Central Management, users in that group were able to log into MetaDefender Endpoint SDP successfully via SSO.

**Recommendation:**

- Avoid using unsupported characters (like &, @, #, etc.) in group names.
- Ensure consistency between Azure AD and My OPSWAT Central Management > External IdP Mapping group names.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
