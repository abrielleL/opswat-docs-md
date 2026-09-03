<!-- source: https://www.opswat.com/docs/mdcore/configuration/error-message-description-table -->

# Error Message Description Table

Every log entry on MetaDefender Core always comes with a message ID number which is an unique identifier for that log entry ( [Log Message Format](/docs/mdcore/configuration/log-message-format))

For example:

log exampleCopy[WARNING] 2019.07.02 05:25:27.749: (core.workflow) Can not send extract task, id='lms::workflow::WorkflowExecutor(0x214af499d00)', node=':1076', block='ExtractBlock' [msgid: 3059]

Then message ID associated to that message would be 3059.

For warning/error message type, besides the message itself (e.g. `Can not send extract task, id='lms::workflow::WorkflowExecutor(0x214af499d00)', node=':1076', block='ExtractBlock'`), using message ID (e.g. 3059) can help reveal more information about that warning/error.

Following is the list of error message description (only applicable to warning/error message type).

Info

Disclaim:

- This list is auto generated and should be updated accordingly with MetaDefender Core upgrade.
- Should be used as reference only, for a complete issue troubleshooting guidance, please reach out to OPSWAT Support.
#### [Error messages need to be monitored](/docs/mdcore/configuration/error-message-description-table#error-messages-need-to-be-monitored)

#### [All error and warning messages](/docs/mdcore/configuration/error-message-description-table#all-error-and-warning-messages)
