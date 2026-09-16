<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-to-remediate-significantly-increased-scanning-times-during-p -->

# How to remediate significantly increased scanning times during peak hours due to engine updates failing?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

**Issue:**

In some cases, automatic engine updates may fail to deploy, causing the engine to be temporarily unavailable. During this time, on-going scans will wait for the response from the failed engine, until it reaches the per AV engine timeout for that engine, or until the engine recovers (whichever comes first).

If this happens during peak hours, it can result in a significant increase in file scanning times, even after the engine recovers.

Example: The Cylance engine is the main contributor to the delay (Cylance ~236ms scan time). Logs show Cylance engine occasionally crashes during updates, causing timeouts and delays at peak hours. This slow processing time can impact production.

**Resolution:**

To avoid such failures from impacting production, we can adjust the engine automatic update schedule to **pause updates during peak hours** to prevent crashes.

Additionally, lowering the Per AV engine timeout, which is a **fail-fast approach**, can avoid lengthy wait times.

**Steps:**

- Navigate to: `Settings > Module update`
- `Pause scheduled updates during:` Add your expected peak hours here

- Navigate to: `Workflow > Metascan > Timeouts`
- `Per AV engine scan:` change to about 15-30 seconds (default is 1 minute)

Info

Lowering the Per AV engine timeout should only be used when the machine specs are not sufficient, and you prioritize speed over a comprehensive result from most licensed engines.

**Verify the change:**

Monitor scan times and engine status during peak hours to ensure the configuration is working as expected and doesn’t cause unwanted AV engine timeouts.

For more information regarding operational impact during engine updates, please refer to this knowledge base: [Will MetaDefender Core Experience Downtime During Engine Updates?](https://www.opswat.com/docs/mdcore/knowledge-base/will-metadefender-core-experience-downtime-during-engine-updates)

Info

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
