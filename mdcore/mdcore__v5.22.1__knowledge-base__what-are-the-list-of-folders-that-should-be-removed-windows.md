<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/what-are-the-list-of-folders-that-should-be-removed-windows -->

# How can I fix a failed or looping MetaDefender Core module update by clearing the package cache?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows systems.

## [When should you use this?](/docs/mdcore/v5.22.1/knowledge-base/what-are-the-list-of-folders-that-should-be-removed-windows#when-should-you-use-this)

- Engine/module updates fail, are stuck, or engines behave inconsistently.
- You need a **full clean reset** of engine and update data to force fresh downloads.
- In some cases, after a license undergoes modifications, remnants of old engines that are no longer reflected in the new license can still exist on the drive.

### [Option A - Standard reset (cached modules/engines)](/docs/mdcore/v5.22.1/knowledge-base/what-are-the-list-of-folders-that-should-be-removed-windows#option-a---standard-reset-cached-modulesengines)

**Stop the service (elevated Command Prompt)**`net stop ometascan`*(Or via* ***Services*** *→* ***OPSWAT MetaDefender Core*** *→* ***Stop***____*.)*

2. **Delete update cache** Delete all contents of: C:\Program Files\OPSWAT\MetaDefender Core\data\updates *(Delete files inside only; keep the folder.)*
3. **Delete engine folders** Delete all contents of: C:\Program Files\OPSWAT\MetaDefender Core\data\engines *(Delete files inside only; keep the folder.)*
4. **Start the service (elevated Command Prompt)**`net start ometascan`*(Or via* ***Services*** *→* ***Start***____*.)*
5. **Trigger module updates** In Core UI go to **Inventory → Modules** and click the **Install all** (blue) button.

6. **Verify** Ensure all modules show **Up to date** and sample scans succeed.

**Linux Systems steps:**

1. **Stop the service (elevated Command Prompt)**`systemctl stop ometascan`
2. **Delete update cache** Delete all contents of: /var/lib/ometascan/updates *(Delete files inside only; keep the folder.)*
3. **Delete engine folders** Delete all contents of: /var/lib/ometascan/engines *(Delete files inside only; keep the folder.)*
4. **Start the service (elevated Command Prompt)**`systemctl start ometascan`
5. **Trigger module updates** In Core UI go to **Inventory → Modules** and click the **Install all** (blue) button.
6. **Verify** Ensure all modules show **Up to date** and sample scans succeed.

### [Option B - Full reset **including old‑license leftovers** *(recommended if engines don’t match entitlements and option A fails to clean the unlicensed engines)*](/docs/mdcore/v5.22.1/knowledge-base/what-are-the-list-of-folders-that-should-be-removed-windows#option-b---full-reset-including-oldlicense-leftovers-recommended-if-engines-dont-match-entitlements-and-option-a-fails-to-clean-the-unlicensed-engines)

1. **Deactivate the Core license** In the Core UI, open the **License** page and **Deactivate**. *(If OCM manages your license, temporarily prevent OCM from auto‑pushing an old license until step 3 is complete.)*
2. **Stop the service (elevated Command Prompt)**`net stop ometascan`*(Or via* ***Services*** *→* ***OPSWAT MetaDefender Core*** *→* ***Stop***____*.)*
3. **Delete update cache** Delete all contents of: C:\Program Files\OPSWAT\MetaDefender Core\data\updates *(Delete files inside only; keep the folder.)*
4. **Delete engine folders** Delete all contents of: C:\Program Files\OPSWAT\MetaDefender Core\data\engines *(Delete files inside only; keep the folder.)*
5. **Start the service (elevated Command Prompt)**`net start ometascan`*(Or via* ***Services*** *→* ***Start***____*.)*
6. **Re‑activate the license** In the Core UI, **Activate** the correct license (online or offline as applicable).
7. **Trigger engine updates** Go to **Inventory → Modules** and click **Install all** (blue button). Core will now download the engine set that matches your license.
8. **Verify** Confirm engines match your entitlements and show **Up to date**.

**Linux Systems steps:**

1. **Deactivate the Core license** In the Core UI, open the **License** page and **Deactivate**. *(If OCM manages your license, temporarily prevent OCM from auto‑pushing an old license until step 3 is complete.)*
2. **Stop the service (elevated Command Prompt)**`systemctl stop ometascan`
3. **Delete update cache** Delete all contents of: /var/lib/ometascan/updates *(Delete files inside only; keep the folder.)*
4. **Delete engine folders** Delete all contents of: /var/lib/ometascan/engines *(Delete files inside only; keep the folder.)*
5. **Start the service (elevated Command Prompt)**`systemctl start ometascan`
6. **Re‑activate the license** In the Core UI, **Activate** the correct license (online or offline as applicable).
7. **Trigger engine updates** Go to **Inventory → Modules** and click **Install all** (blue button). Core will now download the engine set that matches your license.
8. **Verify** Confirm engines match your entitlements and show **Up to date**.

### [Notes](/docs/mdcore/v5.22.1/knowledge-base/what-are-the-list-of-folders-that-should-be-removed-windows#notes)

- This resets **local engine/update data only**; Core configuration remains intact.
- For offline sites, prepare the required offline update packages and license files before you start.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).
