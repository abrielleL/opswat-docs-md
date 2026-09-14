<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/how-to-restrict-user-login-to-mft-based-sso-group-membership- -->

# How to restrict User Login to MFT based SSO Group Membership?

Summarize Page    Connect to Cursor Connect to VS Code Please Note:

OPSWAT supports Single Sign-on (SSO) to the Managed File Transfer application via OIDC only. At present, SAML authentication to MFT is not supported and is not on the roadmap.

[OIDC setup instructions can be found here](/docs/mdmft/v3.11.4/configuration/single-sign-on#requirements)

It's a bit more involved process to support login authorization at a Group level via OIDC than via SAML. There are two ways to go about it.

## [OIDC Provider-side](/docs/mdmft/v3.11.4/knowledge-base/how-to-restrict-user-login-to-mft-based-sso-group-membership-#oidc-provider-side)

This is the ideal approach from a best practice perspective.

Your SSO team can configure your OIDC provider to look at a custom scope field for group membership and only return a successful authentication attempt if the end user belongs to one of the explicitly allow-listed groups.

**Benefits**: All your SSO authorization is handled in a single central location administered by your organization’s standardized processes. Fewer exceptions to manage on a per-application basis.

**Trade-offs**: Depending on your organization, this may be a nontrivial change that requires extensive testing and change windows. Prepare for implementation time to be impacted accordingly.

## [MFT-side](/docs/mdmft/v3.11.4/knowledge-base/how-to-restrict-user-login-to-mft-based-sso-group-membership-#mft-side)

If it’s not feasible for whatever reason, to make the authorization change on your OIDC provider, OPSWAT R&D may be able to help.

Currently the OIDC scopes supported on MFT are only those necessary to verify the user account exists and pull back some non-group related personal info.

However, with enough lead time, it is possible to build other scopes into the MFT UI.

To get started we will need to know 1) the name of your custom group membership scope and 2) how to parse the contents of that scope.

Once we have that information, OSPWAT Support will open an Enhancement Request with R&D. To kick that process off, you will need to open a Support case via [My OPSWAT](https://my.opswat.com/support).

Support will use the case to keep you updated on the feasibility and timeline of implementation.

Once done, you can use the MFT UI to add an explicit list of OIDC groups that are allowed to access the product.

**Benefits**: If your relevant SMEs are otherwise tasked, or their ETA for implementation is too far out for your needs, this approach may provide a much-needed lifeline for your MFT admins, allowing them to specify whole groups to access the application instead of creating unique local accounts for each desired user.

**Trade-offs**: If the Enhancement can be added, the turnaround time is typically several weeks at least, depending on a number of factors. Some of these factors are negotiable on OPSWAT’s end, and your Support Engineer will help you navigate that conversation. Additionally, this is a per-application change that cannot be managed centrally on the SSO-provider side.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
