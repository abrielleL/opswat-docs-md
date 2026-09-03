<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/are-older-antivirus-engine-module-versions-available-for-downgra -->

# Are older antivirus engine module versions available for downgrade?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

## [Overview](/docs/mdcore/v5.21.0/knowledge-base/are-older-antivirus-engine-module-versions-available-for-downgra#overview)

Customers may request to downgrade an antivirus engine module in MetaDefender Core for testing or validation purposes. However, **downgrading is not supported**, and older engine module versions are not maintained or distributed.

Attempting to revert to earlier versions may also introduce compatibility issues, stability concerns, and security risks, particularly when using outdated signatures.

## [Recommendation](/docs/mdcore/v5.21.0/knowledge-base/are-older-antivirus-engine-module-versions-available-for-downgra#recommendation)

For testing or validation scenarios, it is recommended to use the **latest available engine version** and ensure the system can successfully retrieve updates from the update server.

If short-term stability is required (for example, during troubleshooting or investigation), you can **temporarily prevent updates** by pinning the current engine version:

- Navigate to **Inventory > Modules** and confirm the engine and database version currently in use
- Go to **Settings > Module Update** and set updates to *manual* or adjust the schedule to pause updates during your maintenance window
- If using **OPSWAT Central Management**, ensure that central policies do not override these settings

This approach allows you to maintain a consistent environment for testing.

This approach should only be used as a **temporary workaround**. Once testing or troubleshooting is complete, restore automatic updates to ensure the engine continues receiving the latest signatures and security fixes.

Starting from MetaDefender Core v5.19.0, a new **Prevent engine downgrade** setting is available to help protect deployments from unintentionally reverting to older engine or database packages.

When enabled, MetaDefender Core blocks installation of engine or database packages older than the versions currently installed. This helps reduce the risk of outdated threat definitions, compatibility issues, or accidental rollback scenarios.

Please note that intentional engine downgrades are still not officially supported, and older engine packages are not maintained or distributed for rollback purposes.

Support:

If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).
