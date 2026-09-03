<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/how-does-metadefender-managed-file-transfer-protect-against-inje -->

# How does MetaDefender Managed File Transfer protect against injection attacks?

Summarize Page    Connect to Cursor Connect to VS Code
### [How We Prevent SQL Injection](/docs/mdmft/knowledge-base/how-does-metadefender-managed-file-transfer-protect-against-inje#how-we-prevent-sql-injection)

We design the system so that anything you type is treated as harmless data, not as instructions to the database. Here are the safeguards working for you:

- Safe database access: We use placeholders ("parameters") so your input never becomes a command.
- Approved search and sort options: Only known, whitelisted choices are allowed; unexpected values are ignored or sanitized.
- Server-built queries: Flexible queries are assembled from validated pieces on the server, not directly from user-entered text.
- Modern frameworks: Our data access frameworks automatically send your input separately from the SQL instructions.
- Safe error handling: Error messages avoid exposing details about the database or internal systems.
- Ongoing protection: We regularly review, test, and improve these safeguards to keep them effective.

What this means for you: special characters (like quotes or symbols) won’t turn into harmful commands, and your actions are processed safely without requiring you to do anything special.
