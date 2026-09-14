<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/supervisor-approval -->

# Supervisor Approval

Summarize Page    Connect to Cursor Connect to VS Code

Supervisor Approval is a key security feature that enforces an additional layer of control over file access. This feature mandates that supervisors must approve files before users can download or preview them.

Files remain in a "Supervisor Approval" state until approved.

Configuration options for Administrators:

- **One stage:** requires a single approval from any designated supervisor for each file
- **Multi-stage:** allows Administrators to define the total number of approvals required for a file
- **Step-based:** defines a sequence of approval steps, with supervisors sequentially approving the uploaded files
