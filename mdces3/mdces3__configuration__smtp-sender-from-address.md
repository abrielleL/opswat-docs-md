<!-- source: https://www.opswat.com/docs/mdces3/configuration/smtp-sender-from-address -->

# SMTP Sender / From address

Summarize Page

The **Allowlist** feature lets administrators specify trusted sender/From: addresses that should bypass security enforcement to prevent false positives. Emails from allowlisted addresses will not be analyzed or blocked by policy.

## [Adding a Sender/From address Entry](/docs/mdces3/configuration/smtp-sender-from-address#adding-a-senderfrom-address-entry)

1. Select **Sender/From** tab depending on which type of entry to add.
2. Click **Add new entry**
3. Enter the email address (full address, not domain)
4. Specify the allowlist entry scope. Possible values are:

   1. Full Trust (skip all security checks)
   2. Skip multiscanning when enforced by Policy
   3. Skip Sanitization when enforced by Policy
5. (Optional) Add a comment such as: “Trusted vendor”, “Avoids false positives” etc.
6. Click **Save**

The address will now appear in the Allowlist table and will be exempt from scanning enforcement.

## [Editing an Entry](/docs/mdces3/configuration/smtp-sender-from-address#editing-an-entry)

1. Click the **… (actions) menu** next to the entry
2. Select **Edit**
3. Update the email address, scope and/or comment
4. Save changes

## [Removing an Entry](/docs/mdces3/configuration/smtp-sender-from-address#removing-an-entry)

To fully restore scanning enforcement:

1. Click the **… (actions) menu**
2. Select **Delete**
3. Confirm the deletion

Important Notes

- Allowlisting **does not guarantee safety**—it simply bypasses all of parts of the policy enforcement
- Allowlisting is useful for internal systems, trusted partners etc.
