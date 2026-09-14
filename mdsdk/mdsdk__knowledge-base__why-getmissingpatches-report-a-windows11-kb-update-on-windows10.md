<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/why-getmissingpatches-report-a-windows11-kb-update-on-windows10 -->

# Why SDK report a KB update for Windows 11 when using GetMissingPatches on Windows 10?

This article is applied to MetaDefender Endpoint Security SDK releases on **Windows** with **Windows Update Agent (WUA)** Integration.

## [Problem](/docs/mdsdk/knowledge-base/why-getmissingpatches-report-a-windows11-kb-update-on-windows10#problem)

When you run the `GetMissingPatches` method for Windows Update Agent (WUA) on a Windows 10 machine, you may notice updates (`kb_id`) that are associated with Windows 11. This article explains why these appear — specifically focusing on how `upgrade` category updates work and why their KBs point to the newer OS version.

## [What are upgrade updates category?](/docs/mdsdk/knowledge-base/why-getmissingpatches-report-a-windows11-kb-update-on-windows10#what-are-upgrade-updates-category)

As described by Microsoft from [Configure classifications and products](https://learn.microsoft.com/en-us/intune/configmgr/sum/get-started/configure-classifications-and-products):

> *"It specifies an upgrade for Windows 10 or later features and functionality. These updates are also known as feature updates for Windows operating systems."*

Put simply, `upgrade` updates are **the mechanism used to move from one major Windows version to another.** For example, an `upgrade` update allows Windows 10 to move up to Windows 11.

Info

You can read more about how SDK retrieve the categories and other fields directly from WUA in our detailed KB article: [Understanding GetMissingPatches output when invoking with Windows Update Agent (WUA)](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua)

## [Why does the kb_id point to Windows 11 on a Windows 10 machine?](/docs/mdsdk/knowledge-base/why-getmissingpatches-report-a-windows11-kb-update-on-windows10#why-does-the-kb_id-point-to-windows-11-on-a-windows-10-machine)

Normally, the `kb_id` of an update refers to a KB article that applies to the current OS version. This is why many expect the KB to always match Windows 10 if the machine is running Windows 10.

However, `upgrade` updates are different: Their `kb_id` points to the update baseline of **the newer OS version you are upgrading to**, not the current OS.

This is why a Windows 10 machine may show a `kb_id` that actually belongs to Windows 11.

For example, this is an `upgrade` update:

JsonCopy{
"category" : "upgrade",
"category_id" : "3689bdc8-b205-4af4-8d4a-a63924c5e9d5",
"title" : "Windows 11, version 23H2 x64 2025-08B",
"id" : "b5c115e0-a095-46c8-bcfc-23adeab0c0e4",
"preview_patch" : false,
"revision" : 100,
"reboot_required" : true,
"description" : "Install the latest version of Windows: Windows 11, version 23H2.",
"category_description" : "A new product release bringing a device to the next version, containing bug fixes, design changes and new features.",
"product" : "",
"kb_id" : "5063875",
"size" : 1658922382,
"severity" : "unknown",
"optional" : false,
"deployment_action" : 3,
"date" : "1754956800",
"vendor" : "unknown"
}

In this case:

- This update upgrades the OS from **Windows 10** to **Windows 11 23H2**.
- The `kb_id` **(KB5063875)** points to the **update baseline of Windows 11 23H2**, which is the OS you’ll have **after** the upgrade.

According to the Windows 11 23H2 update history at [Windows 11, version 23H2 update history - Microsoft Support](https://support.microsoft.com/en-us/topic/windows-11-version-23h2-update-history-59875222-b990-4bd9-932f-91a5954de434), two additional updates are necessary to keep the OS current with Microsoft's latest release.

This also applies to some other updates as well. Therefore, this is the expected behavior of `upgrade` updates.

Disclaimer

`GetMissingPatches` only **orchestrates WUA results**. Our SDK does not control this behavior. The `kb_id` associated with the upgrade updates may change in the future, as Microsoft often points to the most recent releases.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
