<!-- source: https://www.opswat.com/docs/mdces3/configuration/policies -->

# Policies

Summarize Page

The **Policy View** allows administrators to define, manage, and prioritize email security policies. Policies dictate how inbound and outbound emails are analyzed and handled based on threat detection and prevention technologies.

## [Policy List](/docs/mdces3/configuration/policies#policy-list)

Each row in the policy list provides key details about an individual policy:

- **Policy Name**: The name assigned to the policy for identification.
- **Order**: The ranking of the policy, determining its priority.
- **Direction**: Specifies which email flow the policy applies to:

  - **Inbound**: Emails received by the organization.
  - **Outbound**: Emails sent from the organization.
  - **All Directions**: The policy applies to all email flows.
- **Description**: A brief explanation of what the policy does.
- **Status**: Indicates whether the policy is **Active** or **Inactive**.

### [Policy Application](/docs/mdces3/configuration/policies#policy-application)

- **Drag and Drop Ordering**: Policies are prioritized from top to bottom, with higher policies overriding lower ones in case of conflicts.
- **Only the highest applicable policy** is used when analyzing each email.

### [Managing Policies](/docs/mdces3/configuration/policies#managing-policies)

#### [**Activating or Deactivating Policies**](/docs/mdces3/configuration/policies#activating-or-deactivating-policies)

- Policies can be turned **on or off** using the toggle switch in the **right-most** column.
- **Active Policies**: Are enforced on incoming or outgoing emails.
- **Inactive Policies**: Are not applied to email security processing.

#### [**Reordering Policies**](/docs/mdces3/configuration/policies#reordering-policies)

- Policies can be reordered by dragging and dropping them into the desired priority order.
- The **top-most policy** takes precedence over lower ones in case of conflicting rules.

### [**Default Policy**](/docs/mdces3/configuration/policies#default-policy)

- The **Default Policy** is the baseline policy applied when no other policies match.
- It cannot be moved, deleted or disabled, but can be customized to align with organizational security needs.

## [Policy Details](/docs/mdces3/configuration/policies#policy-details)

### [General Information](/docs/mdces3/configuration/policies#general-information)

This section provides an overview of the policy, including:

- **Policy Name**: A user-defined name for identifying the policy.
- **Description**: A brief explanation of the policy’s purpose.
- **Apply Policy To**: Specifies which email traffic is affected:

  - **Inbound**: Emails received by the organization.
  - **Outbound**: Emails sent from the organization.
  - **All Directions**: The policy applies universally.
- **Status**: Toggle to activate or deactivate the policy.
- **Date Created** and **Last Modified**: Shows when the policy was created and last updated.

### [Policy Summary](/docs/mdces3/configuration/policies#policy-summary)

This section provides a quick summary of the policy configuration, including:

- **Advanced Threat Detection Verdicts**: Displays key threat classifications (e.g., Malicious, Suspicious).
- **Zero-Day Malware Prevention Verdicts**: Displays threat prevention classifications (e.g., Sanitized, Unsupported File Type, Failed Sanitization).
- **Other Processing Outcomes**: Includes additional conditions such as **Encrypted Content** or **Failure to Analyze**.

### [Configuration Settings](/docs/mdces3/configuration/policies#configuration-settings)

The configuration section enables detailed customization of security measures applied by the policy. For more information, see [Verdicts](/docs/mdces3/configuration/verdicts).

#### [Advanced Threat Detection](/docs/mdces3/configuration/policies#advanced-threat-detection)

- **Enabled/Disabled Toggle**: Determines whether OPSWAT Metascan**™**
- Multiscanning is applied.
- **Detection Verdicts**:

  - **Malicious**: High-risk emails detected as harmful.
  - **Suspicious**: Potential threats that require further analysis.
- **Action Options**:

  - **Block**: Prevents email delivery.
  - **Allow**: Permits email delivery despite detection.
- **Configuration**:

  - **Multiscanning engines:** Modify the Anti-Virus engines used in threat detection.

    - **Malicious verdict threshold:** Adjust the number of engines that must trigger to produce a [Malicious](/docs/mdces3/configuration/verdicts#malicious) verdict (Possible values: 1-5).
    - **Suspicious verdict threshold:** Adjust the number of engines that must trigger to produce a [Suspicious](/docs/mdces3/configuration/verdicts#suspicious) verdict (Possible values: 1-5).
  - **MetaDefender Aether:** Enable/disable MetaDefender Aether (Sandbox) analysis for applicable productivity file types.

#### [Zero-Day Malware Prevention](/docs/mdces3/configuration/policies#zero-day-malware-prevention)

- **Configuration Settings**: Defines rules for handling potentially dangerous file content.
- **Processing Outcomes**:

  - **Sanitized:** Emails containing files successfully sanitized.
  - **Unsupported File Type**: Emails containing files that cannot be reconstructed.
  - **Invalid File Structure:** Emails containing files that failed reconstruction due to an unknown/invalid file structure.
  - **Sanitization Policy Error**: Emails containing files that failed reconstruction due to an unspecified reason.
- **Action Options**:

  - **Select**: **Allow** or **Block**.
- **Configuration**:

  - **Sanitization Target:** Select email sanitization scope (bodies, attachments or both).
  - **Exclude Specific File Types from Sanitization:** Select file types to exclude from any sanitization.
  - **Signed Content Exclusions:** Select file types to exclude from any sanitization when signed.
  - **Sanitized Filename Template:** Defines how renamed sanitized files will appear. Variables can be used to preserve metadata while ensuring the filename indicates it has been sanitized.

    - `${original_name}` – The original filename without the extension
    - `${extension}` – The file extension
    - `${timestamp}` – Optional timestamp
    - `${policy_name}` – Optional policy reference
  - **Store original of sanitized email in quarantine:** If enabled, the original unmodified version of the email + attachments is kept in quarantine for investigation or retrieval.

#### [Other Processing Verdicts](/docs/mdces3/configuration/policies#other-processing-verdicts)

- **No Threat Detected:** Emails where no threat was detected and no sanitization took place.
- **Encrypted Content**: Emails containing encrypted attachments.

  - **Action**: **Allow** or **Block**.
- **Failure to Analyze**: Emails that could not be fully examined.

  - **Action**: **Allow** or **Block**.

#### [Additional Settings](/docs/mdces3/configuration/policies#additional-settings)

- **Email Templates**: Configure notification messages for policy enforcement actions.

  - For inbound policies, notifications are delivered to the recipient(s) of the original email.
  - For outbound policies, notifications are delivered to the sender of the original email.
  - **User Permissions:**

    - **Allow users to rescan encrypted content**

      - Allow notification recipient to rescan the email (including providing passwords when any password protected attachments are present in the email).
    - **Allow users to release blocked emails**

      - Allow notification recipient to release a blocked email without administrator approval.
    - **Allow users to view scan result**

      - Allow notification recipient to view the scan results, including any threat names etc.

Info

User Permissions controls what actions can be performed through [User Actions wizard](/docs/mdces3/operating/user-actions).

- **Banner**: Add custom banner to email body based on policy enforcement.

  - Banner location: **Top** or **Bottom** of email body.

### [Target audience](/docs/mdces3/configuration/policies#target-audience)

The **Target Audience** tab allows administrators to define which users or groups a specific policy will apply to. This configuration is crucial for ensuring that the correct set of users are governed by the intended security rules.

The screen is split into two panels:

- **Left Panel – Integrations**: Displays the available integrations, users and groups that can be added to the policy.
- **Right Panel – Selected**: Lists the users and groups currently selected as the target audience for this policy.
- Use the **Search** bar above the Integrations list to quickly locate a specific user or email address.

#### [Add to Target Audience](/docs/mdces3/configuration/policies#add-to-target-audience)

- To assign users/groups to the policy, click the **right arrow (→)** button next to the desired entry in the Integrations panel.
- The selected entry will move to the **Selected** list on the right.

#### [Remove from Target Audience](/docs/mdces3/configuration/policies#remove-from-target-audience)

- To remove a user/group from the policy, click the **left arrow (←)** button next to their entry in the Selected panel.
- The entry will return to the Integrations panel.

#### [Best Practices](/docs/mdces3/configuration/policies#best-practices)

- **Group Selection**: Utilize logical grouping (e.g., departments or teams) for better manageability.
- **Search Filters**: Use precise keywords (email prefix, domain, or name) in the search to quickly locate entries.
- **Regular Review**: Periodically audit the selected audience to ensure policy relevance and security compliance.

Info

The system automatically synchronizes users, groups & group membership with each integration’s directory service approximately every 60 minutes.

### [Additional Filters](/docs/mdces3/configuration/policies#additional-filters)

Use **Additional Filters** to further refine when an inbound content policy is applied. These filters allow you to limit the policy based on the sender and/or specific email headers.

Info

Additional Filters are supported only for **Inbound Policies**.

#### [Sender](/docs/mdces3/configuration/policies#sender)

Enable this option to apply the policy only to emails sent from specific senders.

You can specify:

- Individual email addresses (for example, `user@example.com`)
- Domains (for example, `example.com`)
- Wildcards (for example, `*@example.com`)

If no sender filters are configured, the policy applies to all senders.

#### [Headers](/docs/mdces3/configuration/policies#headers)

Enable this option to apply the policy only when specific email headers are present and match the configured values.

For each header, specify:

- **Header name** — the email header to evaluate
- **Header value** — the expected value for the header

Optionally, enable **Regex** to evaluate the header value using a regular expression instead of an exact match.

Multiple header conditions can be added as needed.

## [Encrypted & Signed Emails](/docs/mdces3/configuration/policies#encrypted--signed-emails)

Emails that are encrypted and/or digitally signed are analyzed when a policy is applied. To preserve message integrity, no modifications (sanitization, banners etc.) are made, as any changes may break the encryption or digital signature.
