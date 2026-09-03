<!-- source: https://www.opswat.com/docs/mdces3/configuration/microsoft-exchange-online -->

# Microsoft Exchange Online

Summarize Page

**MetaDefender Cloud Email Security ™** integrates seamlessly with Microsoft Exchange Online by rerouting email traffic through the platform for advanced security analysis **before** emails reach user mailboxes or are sent externally. This proactive approach enhances protection compared to API-based solutions that scan emails only **after** delivery to the mailbox.

### [**How the Exchange Online Integration Works**](/docs/mdces3/configuration/microsoft-exchange-online#how-the-exchange-online-integration-works)

**MetaDefender Cloud Email Security ™** establishes a mail flow redirection path within Microsoft 365 using the following components:

#### [Outbound Connector](/docs/mdces3/configuration/microsoft-exchange-online#outbound-connector)

Configured in Microsoft 365 to forward selected outbound emails to the product platform for inspection before external delivery.

#### [Inbound Connector](/docs/mdces3/configuration/microsoft-exchange-online#inbound-connector)

Ensures that Microsoft 365 accepts and trusts emails processed and returned from the platform.

#### [Mail Flow Rules (Transport Rules)](/docs/mdces3/configuration/microsoft-exchange-online#mail-flow-rules-transport-rules)

Customizable rules define which emails (inbound or outbound) are rerouted to **MetaDefender Cloud Email Security ™** for analysis. This provides granular control over the protection scope.

For more information see [Integration Details (In-line Protection mode)](/docs/mdces3/configuration/microsoft-exchange-online#integration-details-in-line-protection-mode) and [Integration Details (Monitoring mode)](/docs/mdces3/configuration/microsoft-exchange-online#integration-details-monitoring-mode).

Warning

When integrating on systems with other third-party email security solutions deployed, check [Integrating with 3rd Party Connector-Based Email Security Solutions](/docs/mdces3/knowledge-base/integrating-with-3rd-party-connector-based-email-security-soluti) to ensure accidental email loops are prevented.

#### [Trusted ARC Sealer](/docs/mdces3/configuration/microsoft-exchange-online#trusted-arc-sealer)

**MetaDefender Cloud Email Security ™** platform domain names (opswat.com) are added as Microsoft 365 Trusted ARC sealer domains to ensure trusted communication and prevent emails from being marked as spam or rejected.

## [Wizard Steps](/docs/mdces3/configuration/microsoft-exchange-online#wizard-steps)

This guide walks you through the steps to integrate Microsoft Exchange Online with **MetaDefender Cloud Email Security ™**.

### [Specify Deployment Type](/docs/mdces3/configuration/microsoft-exchange-online#specify-deployment-type)

- You will have two options:

  - **Express**: Will automatically configure a protection integration with default protection settings.
  - **Advanced**: Allows you to customize deployment modes (inline/protected) for a subset of users/groups and set default actions for malicious/suspicious content.

- Select the appropriate option based on your needs.

### [Connect to Microsoft 365](/docs/mdces3/configuration/microsoft-exchange-online#connect-to-microsoft-365)

- Click the **Authorize Application** button.
- This will open the Microsoft 365 sign in page.
- Log in using your **Global Admin Credentials**.
- Grant the required permissions for the platform.

Info

Refer to the [Microsoft 365 Application permissions](/docs/mdces3/knowledge-base/microsoft-365-application-permissions-required) KB article for detailed information on the permissions required by **MetaDefender Cloud Email Security ™**.

### [Define User Protection Scope (Advanced Deployment Only)](/docs/mdces3/configuration/microsoft-exchange-online#define-user-protection-scope-advanced-deployment-only)

- Choose which users will be protected:

  - **All users in the organization** (Apply protection to all accounts)
  - **Only the selected users** (Protect only specific users)
  - **Only the selected groups** (Protect only specific groups)
- Click **Continue** to confirm your selection.

Info

The user protection scope defines which users the Microsoft 365 mail flow rules will apply to. Emails for users not included in this scope will not be routed through **MetaDefender Cloud Email Security ™**. (You can modify the protection scope later through the mail flow rules in the Microsoft 365 Exchange administration center.)

### [How Would You Like Us To Install? (Advanced Deployment Only)](/docs/mdces3/configuration/microsoft-exchange-online#how-would-you-like-us-to-install-advanced-deployment-only)

- Choose how **MetaDefender Cloud Email Security ™** should handle email security:

  - **Protection Mode:** Will actively scan emails in real time.
  - **Monitor Mode**: Receives and analyzes copies of emails for threats, providing detailed reports.
- Select the type of email traffic to be analyzed (You can select one or multiple options):

  - **Inbound** (Incoming emails)
  - **Outbound** (Emails sent outside the organization)
- Click **Continue** to confirm your selection.

### [Summary](/docs/mdces3/configuration/microsoft-exchange-online#summary)

- Verify the selections made is previous steps and confirm by clicking **Continue**.

### [Applying Changes](/docs/mdces3/configuration/microsoft-exchange-online#applying-changes)

- The system will configure the integration.
- You will see status messages indicating successful steps:

  - ✅ Connected to Microsoft Exchange Online.
  - ✅ Configured outbound and inbound connectors.
  - ✅ Configured transport rules.
- Once the system configuration is completed, the mail flow rules can be examined before they are enabled.

  - Refer to [Integration Details (In-line Protection mode)](/docs/mdces3/configuration/microsoft-exchange-online#integration-details-in-line-protection-mode) or [Integration Details (Monitoring mode)](/docs/mdces3/configuration/microsoft-exchange-online#integration-details-monitoring-mode) for more information.

Info

The mail flow rules can also be enabled directly from: [https://admin.exchange.microsoft.com](https://admin.exchange.microsoft.com/). For more details on when using **MetaDefender Cloud Email Security ™** with other 3rd party connector based email security solutions, see: [Integrating with 3rd Party Connector-Based Email Security Solutions](/docs/mdces3/knowledge-base/integrating-with-3rd-party-connector-based-email-security-soluti)

## [Integration Details (In-line protection mode)](/docs/mdces3/configuration/microsoft-exchange-online#integration-details-in-line-protection-mode)

The following changes are applied in your Microsoft 365 environment when integrating with Microsoft 365/Exchange Online.

### [Connectors](/docs/mdces3/configuration/microsoft-exchange-online#connectors)

#### [Inbound connector](/docs/mdces3/configuration/microsoft-exchange-online#inbound-connector)

Used to receive processed emails from **MetaDefender Cloud Email Security ™**.

| Property | Value |
| --- | --- |
| Connector Name | **OPSWAT MetaDefender Cloud Email Security** **- Inbound** |
| From | Partner organization / My organizations own mail server |
| To | Microsoft 365 |
| Identification Method | Sender's IP address |
| Sender IP(s) | [See [Service IP ranges](/docs/mdces3/compliance/locations#service-ip-ranges) ] |
| TLS Settings | Require TLS |
| Restrict to specific domains | No |
| Restrict by certificate | Yes `(*.metadefender.com)` |

#### [Outbound Connector](/docs/mdces3/configuration/microsoft-exchange-online#outbound-connector)

Used to send emails for processing by **MetaDefender Cloud Email Security ™**.

| Property | Value |
| --- | --- |
| Connector Name | **OPSWAT MetaDefender Cloud Email Security** **- Outbound** |
| From | Microsoft 365 |
| To | Partner organization |
| Use of Connector | Only when a mail flow rule routes messages through this connector |
| Smart Host | `ces.metadefender.opswat.com` |
| TLS Settings | Require TLS |
| Validation/Certificate | Yes `(*.metadefender.com)` |
| Routing Method | Route email through smart host |

### [Rules](/docs/mdces3/configuration/microsoft-exchange-online#rules)

#### [Cleanup Headers Rule](/docs/mdces3/configuration/microsoft-exchange-online#cleanup-headers-rule)

This rule will ensure that headers added by **MetaDefender Cloud Email Security ™** are removed from the email before delivery.

| Property | Value |
| --- | --- |
| Rule name | **OPSWAT MetaDefender Cloud Email Security** **- Cleanup** |
| Apply this rule if | - **Sender IP addresses** belong to one of these ranges: [See [Service IP ranges](/docs/mdces3/compliance/locations#service-ip-ranges) ] |
| Do the following | - **Remove** this header: `'X-MDCES-Data'` |
| Stop processing more rules | No |

#### [Allow Rule](/docs/mdces3/configuration/microsoft-exchange-online#allow-rule)

This rule will ensure that emails released from Microsoft 365 Quarantine are delivered.

| Property | Value |
| --- | --- |
| Rule name | **OPSWAT MetaDefender Cloud Email Security** **- Allow** |
| Apply this rule if | - **Sender IP addresses** belong to one of these ranges: [See [Service IP ranges](/docs/mdces3/compliance/locations#service-ip-ranges) ] - `'X-MDCES-PassThrough'` **header** contains `'true'` |
| Do the following | - **Set** the spam confidence level **(SCL)** to '-1' - **Remove** this header: `'X-MDCES-PassThrough'` |
| Stop processing more rules | No |

#### [Inbound Emails Rule](/docs/mdces3/configuration/microsoft-exchange-online#inbound-emails-rule)

This rule triggers for all **inbound** emails.

Info

This rule is only created when inbound email traffic is analyzed.

| Property | Value |
| --- | --- |
| Rule name | **OPSWAT MetaDefender Cloud Email Security** **- Inbound emails** |
| Apply this rule if | - Message is **sent to**: Inside the organization - **From**: Outside the organization |
| Do the following | - **Route the message using connector**: `OPSWAT MetaDefender Cloud Email Security - Outbound` - **Set message header** `X-MDCES-Data` with value: `<Tenant information>` |
| Except if | - **Sender IP addresses** belong to one of these ranges: [See [Service IP ranges](/docs/mdces3/compliance/locations#service-ip-ranges) ] - `'x-ms-exchange-recallreportgenerated'` **header** contains `''true' or 'false''` |
| Stop processing more rules | Yes |

#### [Outbound Emails Rule](/docs/mdces3/configuration/microsoft-exchange-online#outbound-emails-rule)

This rule triggers for all **outbound** emails.

Info

This rule is only created when outbound email traffic is analyzed.

| Property | Value |
| --- | --- |
| Rule name | **OPSWAT MetaDefender Cloud Email Security** **- Outbound emails** |
| Apply this rule if | - Message is **sent to**: Outside the organization - **From**: Inside the organization |
| Do the following | - **Route the message using connector**: `OPSWAT MetaDefender Cloud Email Security - Outbound` - **Set message header** `X-MDCES-Data` with value: `<Tenant information>` |
| Except if | - **Sender IP addresses** belong to one of these ranges: [See [Service IP ranges](/docs/mdces3/compliance/locations#service-ip-ranges) ] - `'x-ms-exchange-recallreportgenerated'` **header** contains `''true' or 'false''` |
| Stop processing more rules | Yes |

## [Integration Details (Monitoring mode)](/docs/mdces3/configuration/microsoft-exchange-online#integration-details-monitoring-mode)

## [Connectors](/docs/mdces3/configuration/microsoft-exchange-online#connectors)

#### [Inbound Connector](/docs/mdces3/configuration/microsoft-exchange-online#inbound-connector)

Used to receive processed emails from **MetaDefender Cloud Email Security ™**.

| Property | Value |
| --- | --- |
| Connector Name | **OPSWAT MetaDefender Cloud Email Security** **- Inbound** |
| From | Partner organization |
| To | Microsoft 365 |
| Identification Method | Sender's IP address |
| Sender IP(s) | [See [Service IP ranges](/docs/mdces3/compliance/locations#service-ip-ranges) ] |
| TLS Settings | Require TLS |
| Restrict to specific domains | No |
| Restrict by certificate | Yes `(*.metadefender.com)` |

#### [Outbound Connector](/docs/mdces3/configuration/microsoft-exchange-online#outbound-connector)

Used to send blind copy (bcc) emails for processing by **MetaDefender Cloud Email Security ™**.

| Property | Value |
| --- | --- |
| Connector Name | **OPSWAT MetaDefender Cloud Email Security** **- Outbound** |
| From | Microsoft 365 |
| To | Partner organization |
| Use of Connector | Use only for email sent to these domains: ‎`metadefender.email‎` |
| Smart Host | `ces.metadefender.opswat.com` |
| TLS Settings | Require TLS |
| Validation/Certificate | Yes `(*.metadefender.com)` |
| Routing Method | Route email through smart host |

### [Rules](/docs/mdces3/configuration/microsoft-exchange-online#rules)

#### [Cleanup Headers Rule](/docs/mdces3/configuration/microsoft-exchange-online#cleanup-headers-rule)

This rule will ensure that headers added by **MetaDefender Cloud Email Security ™** are removed from the email before delivery.

| Property | Value |
| --- | --- |
| Rule name | **OPSWAT MetaDefender Cloud Email Security** **- Cleanup** |
| Apply this rule if |  |
| Apply this rule if | - **Sender IP addresses** belong to one of these ranges: [See [Service IP ranges](/docs/mdces3/compliance/locations#service-ip-ranges) ] |
| Do the following | - **Remove** this header: `'X-MDCES-Data'` |
| Stop processing more rules | No |

#### [Allow Rule](/docs/mdces3/configuration/microsoft-exchange-online#allow-rule)

This rule will ensure that emails released from Microsoft 365 Quarantine are delivered.

| Property | Value |
| --- | --- |
| Rule name | **OPSWAT MetaDefender Cloud Email Security** **- Allow** |
| Apply this rule if | - **Sender IP addresses** belong to one of these ranges: [See [Service IP ranges](/docs/mdces3/compliance/locations#service-ip-ranges) ] - `'X-MDCES-PassThrough'` **header** contains `'true'` |
| Do the following | - **Set** the spam confidence level **(SCL)** to '-1' - **Remove** this header: `'X-MDCES-PassThrough'` |
| Stop processing more rules | No |

#### [Inbound Emails Rule](/docs/mdces3/configuration/microsoft-exchange-online#inbound-emails-rule)

This rule triggers for all **inbound** emails.

Info

This rule is only created when inbound email traffic is analyzed.

| Property | Value |
| --- | --- |
| Rule name | **OPSWAT MetaDefender Cloud Email Security** **- Inbound emails** |
| Apply this rule if | - Message is **sent to**: Inside the organization - **From**: Outside the organization |
| Do the following | - **Blind carbon copy(Bcc) the message to** `bcc-email@metadefender.email` - **Set message header** `X-MDCES-Data` with value: `<Tenant information>` |
| Except if | - **Sender IP addresses** belong to one of these ranges: [See [Service IP ranges](/docs/mdces3/compliance/locations#service-ip-ranges) ] |
| Stop processing more rules | No |

#### [Outbound Emails Rule](/docs/mdces3/configuration/microsoft-exchange-online#outbound-emails-rule)

This rule triggers for all **outbound** emails.

Info

This rule is only created when outbound email traffic is analyzed.

| Property | Value |
| --- | --- |
| Rule name | **OPSWAT MetaDefender Cloud Email Security** **- Outbound emails** |
| Apply this rule if | - Message is **sent to**: Outside the organization - **From**: Inside the organization |
| Do the following | - **Blind carbon copy(Bcc) the message to** `bcc-email@metadefender.email` - **Set message header** `X-MDCES-Data` with value: `<Tenant information>` |
| Except if | - **Sender IP addresses** belong to one of these ranges: [See [Service IP ranges](/docs/mdces3/compliance/locations#service-ip-ranges) ] |
| Stop processing more rules | Yes |
