<!-- source: https://www.opswat.com/docs/mdces3/configuration/files -->

# Files

Summarize Page

The **Allowlist** feature lets administrators specify trusted Files that should bypass security enforcement to prevent false positives.

## [Adding an Entry](/docs/mdces3/configuration/files#adding-an-entry)

1. Select **Files** tab.
2. Click **Add new entry**
3. Enter the SHA256 hash. See [Viewing Event details](/docs/mdces3/operating/events#viewing-event-details) for file hash values.
4. (Optional) Add a comment such as: “Trusted file”, “Avoids false positives” etc.
5. Click **Save**

The file hash will now appear in the Allowlist table and will be exempt from scanning and/or sanitizations.

## [Editing an Entry](/docs/mdces3/configuration/files#editing-an-entry)

1. Click the **… (actions) menu** next to the entry
2. Select **Edit**
3. Update the comment
4. Save changes

## [Removing an Entry](/docs/mdces3/configuration/files#removing-an-entry)

To fully restore scanning enforcement:

1. Click the **… (actions) menu**
2. Select **Delete**
3. Confirm the deletion

Important Notes

- Files **embedded** **within archive files** (e.g., ZIP, RAR, 7z) are not currently supported by attachment hash allowlisting and will not be marked as allowlisted.
- Allowlisting **does not guarantee safety**—it simply bypasses all of parts of the policy enforcement
