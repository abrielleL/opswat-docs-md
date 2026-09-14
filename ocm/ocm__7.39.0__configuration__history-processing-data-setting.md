<!-- source: https://www.opswat.com/docs/ocm/7.39.0/configuration/history-processing-data-setting -->

# History Processing Data synchronization setting

By default, OCM triggers a job to fetch delta history processing data from managed Core instances to allow users access processing data on Core instance from OCM console.

From OCMv7.22 and later, administrators can control this job by updating the file gears-onpremise_definition in the OCM configuration folder

- Windows: C:\ProgramData\OPSWAT\Central\
- Linux: /etc/opt/ocm/

This guideline gives you steps to enable/disable fetching history processing data from managed Core instances.

#### [Enable fetching history processing data from managed Core instances](/docs/ocm/7.39.0/configuration/history-processing-data-setting#enable-fetching-history-processing-data-from-managed-core-instances)

This is enabled by default.

Here are steps to enable this job

- Locate file gears-onpremise_definition in the OCM configuration folder
- Add/Update the key schedule.core.processing.history.enable to "true". Note: if this key is not presented in the file, the key will get its default value as "true"
- (Optional) Add/Update the key schedule.core.processing.history.interval (in milliseconds) to specify how often you would like OCM reaches out to managed Core intances to fetch delta data. Note that if delta data on a Core instance is large, it can impact performance on the Core instance.
- Restart the OCM service

When this job is enabled. OCM tries to fetch delta history processing data from managed Core when

- a user navigates to the history processing page
- a user adds/updates a Core instance on the OCM console
- a user restarts the OCM service
- every N milliseconds, in which N is defined in the key **schedule.core.processing.history.interval **in the file gears-onpremise_definition in the OCM configuration folder. If the key schedule.core.processing.history.interval is not presented in the file, its default value is 1 hour.

#### [Disable fetching history processing data from managed Core instances](/docs/ocm/7.39.0/configuration/history-processing-data-setting#disable-fetching-history-processing-data-from-managed-core-instances)

Here are steps to enable this job

- Locate file gears-onpremise_definition in the OCM configuration folder
- Add/Update the key schedule.core.processing.history.enable to "false".
- Restart the OCM service
