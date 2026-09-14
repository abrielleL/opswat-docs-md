<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/schema-notification-process -->

# Schema Notification Process

## [Abstract](/docs/mdsdk/knowledge-base/schema-notification-process#abstract)

The process is used to notify of upcoming changes in the schema of the various Analog datasets.

## [Purpose of a Notification](/docs/mdsdk/knowledge-base/schema-notification-process#purpose-of-a-notification)

The purpose of the notification is to provide customers with enough knowledge of the upcoming change and enough time so that they can adapt their processing logic to the change correctly.

OPSWAT strives to ensure that the changes in Analog will not break any existing code, though with the notification, customers can prepare for the change(s), ensure that their code will work well with the change(s), and provide feedback to OPSWAT if they have any concerns.

With that said, not all the changes will be notified, and some notifications have different meanings and urgency compared to others.

## [When is a Notification Needed?](/docs/mdsdk/knowledge-base/schema-notification-process#when-is-a-notification-needed)

The notification will happen in either of the following cases:

1. The schema of a server file is changed in a way that will break any schema checks included in Analog package itself (inside `analog/quality_analog/schema/...`). This applies to both bug fixes and feature enhancements.
2. A major feature is introduced requiring new schema.

Therefore, it is recommended that customers **align their schema checks** to match with the published schema in `analog/quality_analog/schema/...`. This ensures that there is no change that may break a customer’s integration without notification.

### [Notification Examples](/docs/mdsdk/knowledge-base/schema-notification-process#notification-examples)

For example, the cases below **will** trigger the notification process:

- A new product will be supported, and to support it requires adding a new field.

  - E.g.: Some association records of product ABC will be added to patch_associations.json, with a new field introduced to better differentiate between different flavors of the product. The schema version of such records will be bumped, the new field will be documented, and sample code will be updated to help the customers integrate with it.
- A major fix that involves a schema change will be released.

  - E.g.: Product ABC has added a new update channel, making existing patching logic (based on patch_associations.json) fail. To fix it, patch association must be enhanced, and it may require updating an existing field in patch_associations.json to contain more values. The schema version of such association records will be bumped, and the document for the field will be updated, together with the sample code.
- A major schema change will be introduced.

  - E.g.: A new feature will be released, and it requires adding a new schema for some data files. The new schema will be documented, and sample code will be updated.

### [No-notification Examples](/docs/mdsdk/knowledge-base/schema-notification-process#no-notification-examples)

And the cases below will **not** trigger any notification:

- A new product will be supported in patching, and to support it does not require adding any new field.

  - E.g.: Product XYZ will be added to patch_associations.json and patch_aggregation.json.
- A minor fix that involves no schema change is released.

  - E.g.: The association record of product XYZ in patch_associations.json will have an optional field added (the field itself is not new).
- A minor change in a feature that does not break the included schema checks is introduced.

  - E.g.: The schema for patch_aggregation.json is updated to limit the length of a string field to 256 characters.

## [The Notification Process](/docs/mdsdk/knowledge-base/schema-notification-process#the-notification-process)

A “notification” is realized as a folder in `analog/changes/` with the name pattern:

`<expected_release_date (yyyy-mm-dd)>_<internal_ticket_id>_<short_description>`

In this folder, there are documents, sample data, new schema, and sample code to explain the change and allow a customer to integrate it easily. A *status file* will also exist to reflect the overall status of the change since its first notification.

For example:

NoneCopyanalog
└──header.json
└──<current folders>
└──changes # contains the notifications
└──2023-11-30_VUL-1111_is_latest (example #1)
└──STATUS # example content:
# UPCOMING_2023-11-30: Change meaning of "is_latest" field
└──HOWTO.pdf
└──sample_code
└──<sample code files>
└──server
└──<server-side data files with the change>
└──client
└──<client-side data files corresponding to the change from server>
└──quality_analog
└──<new schema that reflect the change>
└──2023-12-15_VUL-2222_version_range (example #2)
└──STATUS # example content:
# REVISED_1ST_2023-12-15: Change possible values of "version_range" field
# UPCOMING_2023-12-10: Add new "version_range" field
└──HOWTO.pdf
└──...
└──2023-12-30_VUL-3333_channel_pattern (example #3)
└──STATUS # example content:
# REVOKED_2023-12-30: Do not add "channel" field, waiting for a big revision
# REVISED_1ST_2023-12-30: Change meaning of "channel" field
# UPCOMING_2023-12-15: Add new "channel" field
└──HOWTO.pdf
└──...

When there is a need to make changes in Analog, OPSWAT will implement the change to Release Candidate state, but hold the release to notify the customers about it first, together with the expected release date. On the determined date, OPSWAT releases the change for customers to use.

### [The Detailed Steps](/docs/mdsdk/knowledge-base/schema-notification-process#the-detailed-steps)

The overall process to notify customers about upcoming changes in Analog and the recommended action from the customer is as below, step-by-step:

1. OPSWAT: Put a notification into the Analog package to provide information about the upcoming change (including the expected release date). A *status file* called `STATUS` will exist, with the content describing the change, the history of the change, and the expected release date. Customers should check this file to know the latest status of the change (*UPCOMING*, *REVISED,* or *REVOKED*).

   1. If the change is new and there has been no revision since the first notification, then the content of `STATUS` file will only have a line with “UPCOMING” text (example #1 in *Sample 1*).
2. Customer: Watch for new notifications and integrate with the change if they affect your schema validation or Agent integration.
3. Customer (Optional): If, for some reason, a customer would like to provide feedback or ask about the release date, you may create a support ticket on OPSWAT Portal and prefix the case’s title with “Analog Feedback”.
4. OPSWAT: Prioritize answering feedback from customers in step 3, such as not blocking their integration. There are some situations that may be raised:

   1. Revisions: Based on customer feedback, OPSWAT may revise the change. Each time the change is revised, the `STATUS` file will contain `REVISED_<time of revision>` to signify the revision (example #2 in *Sample 1*).
   2. Revoke: A change may be revoked after its notification (and before the release date). In that case, the `STATUS` file will contain a `REVOKED` line (example #3 in *Sample 1*).
5. OPSWAT: On the expected date, OPSWAT will release the Analog package containing the change(s). The notification is kept for 1 month after a release for easy tracking.
6. OPSWAT: About 1 month after the change is applied, the notification folder is removed.

The process is visualized in the flow chart below:

## [Notification Timeline](/docs/mdsdk/knowledge-base/schema-notification-process#notification-timeline)

Depending on the nature of the change, some schema changes may be released faster than others.

There are two main kinds of schema changes:

1. **Hot fix:** Urgent fixes that need to be released very soon. If that requires a notification for some reason, then the notification will be at least 1 calendar week before release.
2. **Planned release:** Non-urgent fixes or feature enhancements. The notification will be at least 2 calendar weeks before the release.
