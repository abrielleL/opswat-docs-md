<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/configuration/activate-supervisor-approval-process -->

# Activating the Supervisor Approval Process

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Activating the Approval Process](/docs/mdmft/v3.11.5/configuration/activate-supervisor-approval-process#activating-the-approval-process)

1. Go to "Supervisor Approval" → "Process Setup."
2. Create a Draft process configuration. If previously activated, the existing draft can be edited
3. Modify the process configuration according to the "Supervisor Approval Settings", "Supervisor Setup", and the "Active Directory Supervisors Setup" pages.
4. Activate the draft.

Info

The approval process is only active if there is an active configuration. Without an active configuration or with only a draft, the approval process is disabled.

Supervisor Approval disabled: No previous configuration

Supervisor Approval disabled: Previous configuration exists

Activate the draft to enable supervision

Note

Drafts are automatically saved during setup.

## [Editing an Existing Approval Process Configuration](/docs/mdmft/v3.11.5/configuration/activate-supervisor-approval-process#editing-an-existing-approval-process-configuration)

Changes can be made to the draft while the current configuration remains active.

Warning

When the draft is activated, it replaces the active configuration. The previous configuration is not saved and cannot be restored.

Supervision is enabled

Supervision is enabled: A new process configuration has been created

## [Disabling the Approval Process](/docs/mdmft/v3.11.5/configuration/activate-supervisor-approval-process#disabling-the-approval-process)

Disabling the Active process configuration also disables the approval process.

Note

The disabled configuration is saved as a draft for potential reactivation.

Warning

If a draft already exists, it will be discarded to preserve the deactivated configuration.

## [Previewing the Active Approval Process](/docs/mdmft/v3.11.5/configuration/activate-supervisor-approval-process#previewing-the-active-approval-process)

The active configuration can be viewed in read-only mode.

Info

Preview access is available even when another user is editing the draft.

## [Simultaneous Multiple Users Configuration](/docs/mdmft/v3.11.5/configuration/activate-supervisor-approval-process#simultaneous-multiple-users-configuration)

When a user begins editing the configuration, it is locked to prevent simultaneous changes. The lock is released after 30 minutes of inactivity.

The draft can also be manually discarded to allow another user to begin editing.

Warning

Draft editing and Active Directory synchronization are mutually exclusive. Only one can run at a time; the other must wait until the current task is complete.

Supervision enabled: Someone else is editing the configuration
