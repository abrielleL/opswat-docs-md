<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-can-i-fix-a-failed-or-looping-metadefender-core-module-updat -->

# How can I fix a failed or looping MetaDefender Core module update in MyOPSWAT Central Management v10 by clearing the package cache?

This article applies to all MyOPSWAT Central Management v10 releases deployed on Windows systems.

## [**When should you use this?**](/docs/mdcore/v5.22.0/knowledge-base/how-can-i-fix-a-failed-or-looping-metadefender-core-module-updat#when-should-you-use-this)

- Modules under **Settings → Update Package → Modules** fail, stall, or loop.
- You want My OCM v10 to re-download **all** **module packages** from scratch.

## [**What this does?**](/docs/mdcore/v5.22.0/knowledge-base/how-can-i-fix-a-failed-or-looping-metadefender-core-module-updat#what-this-does)

Clears OCM’s local **package cache** and restarts the service so OCM repopulates it with fresh packages. Your OCM configuration and product inventory remain unchanged.

## [**Steps required:**](/docs/mdcore/v5.22.0/knowledge-base/how-can-i-fix-a-failed-or-looping-metadefender-core-module-updat#steps-required)

1. Change the update source to **Manual**
   Open Settings → Update Package → Modules → Source → set it to manual → click Save
2. **Stop the service**
   Open **Services** → find **My OPSWAT Central Management** → right‑click **Stop**.
   *(Run Services as Administrator.)*
3. **Clear cached packages**
   Delete the contents of:
   `C:\Program Files\OPSWAT\MOCM\data-agent\fusion-updater`
   `C:\Program Files\OPSWAT\MOCM\data-agent\mdcore`
   *(Delete files inside only; keep the folder.)*
4. **Start the service**
   In **Services**, right‑click **My OPSWAT Central Management** → **Start**.
   *(Run Services as Administrator.)*
5. Change the update source to **Internet**
   Open Settings → Update Package → Modules → Source → set it to Internet → click Save
6. **Trigger module updates**
   After saving the settings, within the same page, press the **Update Now** button.
   *(The modules list might still be populated with the old versions even after deleting the cached files, but they will get updated once finishing this step.)*
7. **Verify**
   Confirm all module packages download and show **Up to date** status.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).
