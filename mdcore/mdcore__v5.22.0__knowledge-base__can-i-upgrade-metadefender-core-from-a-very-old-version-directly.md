<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/can-i-upgrade-metadefender-core-from-a-very-old-version-directly -->

# Can I upgrade MetaDefender Core from a very old version directly to the latest available?

Before upgrading to the latest version of MetaDefender Core, please make sure that all the System Requirements and the prerequisites of the newer version are met.

It is very important to consider that very old versions of MetaDefender Core - especially those that are no longer supported (see [MetaDefender Core Support Lifecycles](/docs/mdcore/v5.22.0/knowledge-base/how-long-is-the-support-life-cycle-for-a-specific-version-releas)) - may not be able to upgrade directly to the latest available version. This limitation can arise from a variety of factors, such as changes in database schemas, altered data relationships, third-party dependency updates, and other architectural differences.

In this case, when speaking of a large gap of versions between the current one and the latest, our recommendation is to incrementally upgrade the application, from close to close (for example, 3 or 2 versions at a time), to successfully guarantee a smooth upgrade path.

If running an out-of-support version ([MetaDefender Core Support Lifecycles](/docs/mdcore/v5.22.0/knowledge-base/how-long-is-the-support-life-cycle-for-a-specific-version-releas)) or for any additional support on this, please do not hesitate to reach out to our Support Team which can assist you with the upgrade process.

Info:

We do always recommend having a back-up solution in place before proceeding with any upgrade. Taking a snapshot of the machine(s) holding the component(s) [application/database] is recommended.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
