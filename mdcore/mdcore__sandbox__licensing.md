<!-- source: https://www.opswat.com/docs/mdcore/sandbox/licensing -->

# Licensing

This page applies to the **Embedded Aether (Adaptive Sandbox)** engine version **2.2.0** and above.

## [License Usage and Execution Limits](/docs/mdcore/sandbox/licensing#license-usage-and-execution-limits)

Your MetaDefender Core license includes a **daily execution limit** for the **Embedded Aether (Adaptive Sandbox)** engine, which determines the maximum number of scans that can be performed within a single day. The execution count resets at midnight (UTC).

Warning

Restart the engine after activating a new license for the changes to take effect. Current scan count will not reset on license actions.

### [Soft Limit (Warning)](/docs/mdcore/sandbox/licensing#soft-limit-warning)

Your license allows exceeding the limit by 20%. During this period, known as the **soft limit**, the system will continue to allow scans but will display a warning indicating the remaining available executions.

### [Hard Limit (Enforcement)](/docs/mdcore/sandbox/licensing#hard-limit-enforcement)

If the number of executed scans exceeds 120% of the daily limit, the **hard limit** is enforced, and further executions will be blocked until the next day. A license error will be returned, preventing additional scans.

## [Overuse Adjustment](/docs/mdcore/sandbox/licensing#overuse-adjustment)

If the soft limit is reached for 7 consecutive days, the soft limit will become the hard limit, effectively reducing the maximum number of scans allowed per day. The original soft limit is reverted the next day if the scan limit is not reached.

## [Example Scenarios:](/docs/mdcore/sandbox/licensing#example-scenarios)

License limit: 100 scans/day

Soft limit: 101-120 scans → Warning displayed, but scans continue.

Hard limit: 121+ scans → Execution blocked until midnight.

If soft limit is reached 7 consecutive days → New hard limit set to 100 scans/day, and the 20% buffer is no longer available. Warning zone starts with scan number 81.

Ensure that your scanning usage stays within acceptable limits to avoid disruptions. If you require more executions, consider upgrading your license.
