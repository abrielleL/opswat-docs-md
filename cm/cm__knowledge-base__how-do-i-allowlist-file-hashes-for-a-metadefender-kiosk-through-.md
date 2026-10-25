<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-allowlist-file-hashes-for-a-metadefender-kiosk-through- -->

# How do I allowlist file hashes for a MetaDefender Kiosk through My OPSWAT Central Management?

> **Check Your Version:**
>
> This article applies to MetaDefender Kiosk (Windows and Linux) enrolled to My OPSWAT Central Management 10, processing files through MetaDefender Core.

### Overview

Administrators often want a specific file to pass through a Kiosk without being scanned or blocked — a known-good utility, a signed installer, or a file repeatedly flagged as a false positive.

The **Skip By Hash** feature in My OPSWAT Central Management manages hash lists for **MetaDefender Core** instances. There is no Kiosk-targeted hash list.

This is not a limitation in practice. A Kiosk does not scan files itself — it submits them to the MetaDefender Core instance configured for it, and Core returns the verdict. A hash rule applied on that Core therefore governs files submitted by the Kiosk. **Allowlist the hash on the Core that serves your Kiosk.**

This applies equally to Kiosk on Windows and Kiosk on Linux, because the mechanism sits on the Core side.

### Option 1 — Centrally, through Central Management

Use this when you manage several Core instances, or want one list maintained in one place.

1. In Central Management, go to **Inventory → Skip By Hash** and create a hash list.
2. Add entries. Each entry takes an action:
   - **Allowlist** — the file is allowed and scanning is skipped
   - **Blocklist** — the file is denied without being scanned
   - **Skip Engines** — the file is scanned, but the engines you name are excluded
3. Open the list's **Assignments** tab and assign it to the **Core policy** that governs the Core instance serving your Kiosk. A list has no effect until it is assigned.
4. Verify: open that Core policy and check its **Skip By Hash** tab, which shows the entries reaching the policy.

Changes synchronise automatically and incrementally. An instance that is offline picks up the changes when it next connects.

Reference: [https://www.opswat.com/docs/cm/product-management/skip-by-hash](https://www.opswat.com/docs/cm/product-management/skip-by-hash)

**Note:** a policy can carry only one hash list. Assigning a second list to a policy replaces the first one without a warning, and the instances under that policy resync to the new list. Check the Assignments tab after making changes.

### Option 2 — Locally, on the Core instance

Use this for a single Core, or where the Core is not centrally managed.

On the Core Management Console, go to **Inventory → Skip by Hash** and add the hash to the **Allowlist**. Hashes can be added manually or imported from CSV.

Core's hash lists are applied **globally**, not per workflow — an allowlisted file is allowed regardless of which workflow processes it.

Reference: [https://www.opswat.com/docs/mdcore/operating/inventory-management](https://www.opswat.com/docs/mdcore/operating/inventory-management)

### If the hashes do not take effect

The most common cause is the Core-side setting that controls whether an instance accepts its skip-hash configuration from Central Management. This setting lives on the **Core instance**, and it cannot be viewed or changed from Central Management.

Check it on the Core itself before investigating further. When it is enabled, Central Management becomes the source of truth for that instance and local hash management on the Core becomes read-only.

### Which hash type to use

Core accepts MD5, SHA1, SHA256 and SHA512. **SHA256 is recommended** for new entries.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
