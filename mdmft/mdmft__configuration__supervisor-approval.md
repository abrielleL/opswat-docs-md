<!-- source: https://www.opswat.com/docs/mdmft/configuration/supervisor-approval -->

# Supervisor Approval

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Supervisor Approval is a key security feature that enforces an additional layer of control over file access. This feature mandates that supervisors must approve files before users can download or preview them.

Files remain in a "Supervisor Approval" state until approved.

Configuration options for Administrators:

- **One stage:** Requires a single approval from any designated supervisor for each file.
- **Multi-stage:** Allows Administrators to define the total number of approvals required for a file.
- **Step-based:** Defines a sequence of approval steps, with supervisors sequentially approving the uploaded files.
- **Manager-based:** A variant of the Step-based approach, where direct managers from Active Directory will act as designated supervisors for each user on the first step. Additional steps may also be defined where it is only possible to elect default supervisors.
