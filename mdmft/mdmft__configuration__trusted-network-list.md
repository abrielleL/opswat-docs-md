<!-- source: https://www.opswat.com/docs/mdmft/configuration/trusted-network-list -->

# Trusted Network List

Summarize Page    Connect to Cursor Connect to VS Code

The "Trusted Network List" feature allows administrators to configure network rules, applying upload or download restrictions based on users' IP addresses.

### [Default Rule](/docs/mdmft/configuration/trusted-network-list#default-rule)

A default rule (0.0.0.0/0) is always configured. This rule applies to all IP addresses unless other rules are specified.

You can use this rule to deny uploads or downloads for everyone and then create specific rules to permit uploads or downloads for certain IP addresses.

### [Adding a New Rule](/docs/mdmft/configuration/trusted-network-list#adding-a-new-rule)

To add a rule, click the "Add new rule" button and complete the required fields on the pop-up modal.

The following options are available:

1. Add a rule for a specific IP address (i.e. 192.168.16.20)
2. Add a rule for a range of IP addresses using CIDR notation (i.e 192.168.16.0/24)

   1. You can configure up to five exception IP addresses to this rule.

The restrictions available for each rule include:

1. Upload and/or download limitations for specific IP addresses:

   1. Allowed for all users
   2. Denied for all users
   3. Allowed for selected groups only (BETA) *
   4. Denied for selected groups only (BETA) *
2. Enable or disable password reset requests for specific IP addresses
3. Allow authentication from specific IP addresses

Info

- Select group-based limitations only if Custom Groups or Active Directory Groups have been added. Only members of the selected groups can or cannot upload/download files depending on restrictions.
### [Preferred Sign-In Method](/docs/mdmft/configuration/trusted-network-list#preferred-sign-in-method)

You can choose which login tab appears first on the login page: Normal Sign-in (used by local users, AD users, SSO users, or external users), Radius Sign-in, or Guest User Sign-in.

### [Enable Auto-Redirect to SSO Provider](/docs/mdmft/configuration/trusted-network-list#enable-auto-redirect-to-sso-provider)

Enabling this option will automatically redirect users to the SSO provider for login when they access the MetaDefender Managed File Transfer login page.

Info

Auto redirection is bypassed when the application is accessed from the MetaDefender Managed File Transfer™ server machine, ensuring that local administrators can log in if the SSO provider is unavailable.

### [Add exception IP](/docs/mdmft/configuration/trusted-network-list#add-exception-ip)

Trusted Network rules configured for custom IP address ranges support the definition of up to five exception IP addresses per range. When a user accesses MFT from an exception IP, a different set of rule behaviours e applied. This can impact functionalities such as authentication, password reset, automatic redirection to the SSO provider, as well as file upload and download operations.

Info

For the features listed below, the default Trusted Network rule will apply when MFT is accessed from an exception IP address:

- Auto Redirect to SSO Provider
- Password Reset
- Allowed Authentication Types

For upload and download rules, the behaviour for exception IP addresses is inverted relative to the configured rule for the IP address range.

**For example, if the configured rules are:**

Upload: Allowed for all users

Download: Denied for all users

Then, when accessed from an exception IP address, the applied rules will be:

Upload: Denied for all users

Download: Allowed for all users

**For example, if the configured rules are group based:**

Upload: Allowed for selected groups only

Download: Denied for selected groups only

Then, when accessed from an exception IP address, the applied rules will be:

Upload: Denied for selected groups only

Download: Allowed for selected groups only

### [Rule Management](/docs/mdmft/configuration/trusted-network-list#rule-management)

To find rules configured for a specific IP address, use the 'Search for network address' field. For more detailed search options click on the "Advanced" button, select one or multiple desired search option, then click on the "Apply" button.

Table view with applied "Download: Denied for all users" option

To remove the applied search option just click the "X" on the label.

Bulk action are available for deleting multiple rules at once.
