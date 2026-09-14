<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/why-does-oesis-detect-ms-teams-but-only-patch-some-variants -->

# Why Does OESIS Detect Microsoft Teams But Only Patch Some Variants on Windows?

## [Overview](/docs/mdsdk/knowledge-base/why-does-oesis-detect-ms-teams-but-only-patch-some-variants#overview)

OESIS detects three distinct Microsoft Teams signatures on Windows. Only two of them support patch management. This article explains the reason behind each case and how developers should handle signature mapping in their remediation workflows.

---

## [The Three Windows Teams Signatures](/docs/mdsdk/knowledge-base/why-does-oesis-detect-ms-teams-but-only-patch-some-variants#the-three-windows-teams-signatures)

| Signature ID | Signature Name | Patch Supported |
| --- | --- | --- |
| **3089** | Microsoft Teams classic | Yes |
| **3797** | Microsoft Teams work or school | Yes |
| **3799** | Microsoft Teams | No |

---

## [Why Sig 3089 (Classic) and 3797 (Work or School) Support Patching](/docs/mdsdk/knowledge-base/why-does-oesis-detect-ms-teams-but-only-patch-some-variants#why-sig-3089-classic-and-3797-work-or-school-support-patching)

Both of these variants are distributed by Microsoft through a **publicly accessible installer**. OPSWAT can obtain and reference the installer URL, track new releases, and automate download and installation through the SDK patching workflow. This is what makes patching possible — the availability of a direct, stable distribution channel that OPSWAT can integrate with.

- Sig **3089** (Classic Teams, version 1.x) uses a traditional Win32 EXE installer.
- Sig **3797** (New Teams, version 2x.x) uses an MSIX package installer.

Both have `support_3rd_party_patch: true` and `usable_download_link: true` in the Analog `products.json`, and both have a corresponding entry in `patch_associations.json` mapping them to a downloadable patch.

---

## [Why Sig 3799 (Microsoft Teams) Does Not Support Patching](/docs/mdsdk/knowledge-base/why-does-oesis-detect-ms-teams-but-only-patch-some-variants#why-sig-3799-microsoft-teams-does-not-support-patching)

Sig 3799 corresponds to the **personal/consumer edition** of Microsoft Teams, distributed exclusively through the **Microsoft Store**. Microsoft does not provide a publicly accessible standalone installer for this variant — updates are managed entirely by the Store's own update mechanism.

Because there is no accessible installer URL, OPSWAT cannot build a patch entry for it. This is reflected directly in the Analog data:

JsonCopy{
"id": 3799,
"name": "Microsoft Teams",
"support_3rd_party_patch": false,
"usable_download_link": false
}

There is also no entry for signature 3799 in `patch_associations.json`, meaning the SDK will not return a patch ID or download URL when this signature is queried.

---

## [Developer Note: Mapping Signatures Correctly in Remediation Workflows](/docs/mdsdk/knowledge-base/why-does-oesis-detect-ms-teams-but-only-patch-some-variants#developer-note-mapping-signatures-correctly-in-remediation-workflows)

When building a remediation workflow, developers must not assume that all detected Teams signatures are patchable. The recommended approach is to explicitly allow-list only the signatures that support patching and skip any others before triggering patch APIs.

Based on the current Analog data, the correct mapping is:

| Signature ID | Include in Patch Workflow? |
| --- | --- |
| 3089 | Yes |
| 3797 | Yes |
| 3799 | No — skip, do not call `GetLatestInstaller` or `InstallFromFile` |

### [Client-Side Filtering — Using `patch.dat` and `LoadPatchDatabase`](/docs/mdsdk/knowledge-base/why-does-oesis-detect-ms-teams-but-only-patch-some-variants#client-side-filtering--using-patchdat-and-loadpatchdatabase)

As described in the [How to Identify Automatic vs Manual Patching Using Analog Files](https://www.opswat.com/docs/mdsdk/knowledge-base/how-to-identify-automatic-vs-manual-patching-using-analog-files) KB article, after loading `patch.dat` via `LoadPatchDatabase`, the response includes the following fields:

| Field | What it contains |
| --- | --- |
| `details.support_signatures` | Signatures fully supported for automatic patching (`GetLatestInstaller` + `InstallFromFiles`) |
| `details.support_install_signatures` | Signatures supported for manual patching only (`InstallFromFiles` only) |
| `details.self_update_signatures` | Signatures where automatic patching is supported but only for installer download, not URL |

Because sig 3799 has `support_3rd_party_patch: false`, it will **not appear in any of these lists**. Sigs 3089 and 3797 will appear in `details.support_signatures`, confirming they support the full automatic patching workflow.

The correct approach is to check the signature returned by `GetProductInfo` against `details.support_signatures` before proceeding with patching. If the detected signature is not in that list, skip the patch workflow entirely.

### [Server-Side Filtering — Using `products.json`](/docs/mdsdk/knowledge-base/why-does-oesis-detect-ms-teams-but-only-patch-some-variants#server-side-filtering--using-productsjson)

On the server side, check the `support_3rd_party_patch` field per signature in the `products.json` before sending any patch instruction to the client. If the field is `false` for the detected signature, the remediation workflow should not be triggered.
