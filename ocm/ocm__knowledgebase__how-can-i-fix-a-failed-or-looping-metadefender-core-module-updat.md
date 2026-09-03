<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/how-can-i-fix-a-failed-or-looping-metadefender-core-module-updat -->

# How can I fix a failed or looping MetaDefender Core module update in OCM v7 by clearing the package cache?

This article applies to all OPSWAT Central Management v7 releases deployed on Windows systems.

## [When should you use this?](/docs/ocm/knowledgebase/how-can-i-fix-a-failed-or-looping-metadefender-core-module-updat#when-should-you-use-this)

- Updates under **Inventory → MetaDefender Core Modules** fail, stall, or loop.
- You want OCM to re-download **all** module packages from scratch.

## [What this does?](/docs/ocm/knowledgebase/how-can-i-fix-a-failed-or-looping-metadefender-core-module-updat#what-this-does)

Clears OCM’s local **package cache** and restarts the service so OCM repopulates it with fresh packages. Your OCM configuration and product inventory remain unchanged.

## [Steps required:](/docs/ocm/knowledgebase/how-can-i-fix-a-failed-or-looping-metadefender-core-module-updat#steps-required)

1. **Stop the service** Open **Services** → find **OPSWAT Central Management** → right‑click **Stop**. *(Run Services as Administrator.)*
2. **Clear cached packages** Delete the contents of: `C:\Program Files\OPSWAT\Central\tomcat\webapps\core\package\`*(Delete files inside only; keep the folder.)*
3. **Start the service** In **Services**, right‑click **OPSWAT Central Management** → **Start**.
4. **Trigger module updates** In OCM UI go to **Inventory → MetaDefender Core Modules** and click **Update now** (blue button).

1. **Verify** Confirm all module packages download and show **Up to date** status.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).
