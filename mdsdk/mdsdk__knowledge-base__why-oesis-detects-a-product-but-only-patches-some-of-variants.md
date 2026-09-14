<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/why-oesis-detects-a-product-but-only-patches-some-of-variants -->

# Why OESIS Detects a Product but Only Patches Some of Its Variants

## [Summary](/docs/mdsdk/knowledge-base/why-oesis-detects-a-product-but-only-patches-some-of-variants#summary)

A product supported by OESIS Framework may exist in multiple **variants** — different architectures, installer types, distribution channels, or release lines. Each variant is mapped to its own **OESIS signature**, and only some of those signatures support patching. As a result, OESIS may detect every variant of a product but only be able to patch some of them.

This article explains how OESIS represents product variants, the known categories of variants that cannot be patched and why, how to identify which variant is installed, and how to request patching support for a variant that is not covered by the categories below.

## [How OESIS represents products and signatures](/docs/mdsdk/knowledge-base/why-oesis-detects-a-product-but-only-patches-some-of-variants#how-oesis-represents-products-and-signatures)

In the OESIS product database (the `analog/server/products.json` file shipped with OESIS), a **product** (for example, *Microsoft Teams*) is an umbrella for one or more **signatures**. A signature identifies one specific variant of the product — for example, a specific OS architecture (x86, x64, ARM64), installer technology (EXE, MSI), installation scope (per-machine, per-user), distribution channel (desktop installer vs. Microsoft Store), or major release line (e.g., Java 7 vs. Java 8).

Patching support is defined **per signature**, not per product (the `support_3rd_party_patch` attribute in `products.json`). Two installations of "the same product" can therefore match different signatures — and only one of them may be patchable.

> **Example — Microsoft Teams on Windows.** OESIS supports three signatures for Teams: *Microsoft Teams classic*, *Microsoft Teams work or school*, and *Microsoft Teams* (the new Teams app distributed through the Microsoft Store). The first two support patching; the Microsoft Store variant does not. An installation of the Store variant is detected but not patchable, while an installation of Teams work or school can be patched normally.

## [Why some signatures cannot be patched](/docs/mdsdk/knowledge-base/why-oesis-detects-a-product-but-only-patches-some-of-variants#why-some-signatures-cannot-be-patched)

### [1. Microsoft Store (UWP) applications](/docs/mdsdk/knowledge-base/why-oesis-detects-a-product-but-only-patches-some-of-variants#1-microsoft-store-uwp-applications)

OESIS Framework does not support patching UWP applications distributed through the Microsoft Store. These signatures are **detection-only**. Remediation options:

- Allow the Microsoft Store to update the application, or
- Migrate to the vendor's desktop-installer variant of the same product, which OESIS can patch.

Examples of Microsoft Store / UWP signatures that are detection-only:

| Product | Signature name | Signature ID |
| --- | --- | --- |
| Microsoft Teams | Microsoft Teams | 3799 |
| Mozilla Firefox | Mozilla Firefox UWP | 3995 |
| iTunes | iTunes UWP | 4114 |
| Splashtop Business | Splashtop Business UWP | 3939 |
| Splashtop Personal | Splashtop2 Personal UWP | 3919 |
| Splashtop Personal | Splashtop Personal UWP | 3940 |
| myViewBoard Whiteboard | myViewBoard Whiteboard 3+ UWP | 4101 |
| Yubico Authenticator | Yubico Authenticator UWP | 4116 |

*The current status of the applications listed above is based on the data available as of July 28, 2026.*

### [2. Variants discontinued by the vendor](/docs/mdsdk/knowledge-base/why-oesis-detects-a-product-but-only-patches-some-of-variants#2-variants-discontinued-by-the-vendor)

Some signatures cover a variant that the vendor no longer ships — a retired architecture, an abandoned installer format, or a discontinued edition. Because no current installer exists for that variant, there is nothing OESIS can patch **to**: the newest version available for that variant is already the last version that will ever exist.

These signatures remain in the database so that OESIS can still **detect** the (now outdated) software and report it, which is valuable for vulnerability assessment. Remediation is migration to the vendor's supported variant.

Examples:

| Product | Discontinued variant (detection-only) | Supported path |
| --- | --- | --- |
| Blender | Blender x86 | Blender x64 |
| Microsoft Power BI Desktop | Microsoft Power BI Desktop x86 | Microsoft Power BI Desktop x64 |
| CDBurnerXP | CDBurnerXP msi x64, CDBurnerXP msi x86 | CDBurnerXP x64, CDBurnerXP x86 |
| LogMeIn Rescue Technician Console | LogMeIn Rescue Technician Console | LogMeIn Rescue Technician Console App |

*The current status of the applications listed above is based on the data available as of July 28, 2026.*

### [3. End-of-life release lines](/docs/mdsdk/knowledge-base/why-oesis-detects-a-product-but-only-patches-some-of-variants#3-end-of-life-release-lines)

Many vendors maintain several release lines of a product in parallel and eventually stop servicing the older lines. OESIS tracks major release lines as separate signatures. OESIS can continue to support patching a release line as long as the vendor still maintains installers for it; once the vendor stops maintaining installers for that line, OESIS must stop patching support and the signature becomes detection-only. Moving to a serviced line is an **upgrade/migration decision** (potentially with licensing, compatibility, or workflow implications), which OESIS does not perform automatically as a patch.

Remediation: plan a migration to a release line that the vendor still services; OESIS can patch the installation from then on.

Examples of end-of-life or superseded lines that are detection-only:

| Product | Detection-only line(s) | Patchable line(s) |
| --- | --- | --- |
| Java (Oracle) | Java 6, 7, 9, 10 | Java 8 (x86/x64) |
| Microsoft Office (Click-to-Run) | Office 2013 | Office 2016 / 2019 / 2021 / 2024 |
| Microsoft Edge | Edge Legacy (EdgeHTML) | Edge 80+ (Chromium) |
| Microsoft Teams (macOS) | Teams classic | Teams work or school |
| Beyond Compare | Beyond Compare 1, 2 | Beyond Compare 3, 4 |
| Sublime Text | Sublime Text 2 | Sublime Text 3 |
| Snagit | Snagit legacy releases | Snagit 2022 / 2023 / 2024 |
| SQL Server Management Studio | SSMS legacy | SSMS 19 |
| Nitro Pro | Nitro Pro 11, 12 | Nitro Pro 13 |
| Adobe Digital Editions | ADE 2.0, 3.0, 4.0 | ADE 4.5 |
| pgAdmin 4 | pgAdmin 4 v3 | pgAdmin 4 v4–v9 |
| TeamViewer / TeamViewer Host | Legacy versions, Host 10–14 | Current versions, Host 15 |
| Box Sync | Box Sync (legacy) | Box Sync 4+ |
| 1Password | 1Password (legacy) | 1Password 6+ |

*The current status of the applications listed above is based on the data available as of July 28, 2026.*

OESIS provides the `IsDefunct` method to programmatically identify end-of-life (defunct) products, so integrations can detect when an installed release line has reached end of life and plan the migration to a supported line. See the [OESIS V4 method documentation](https://software.opswat.com/OESIS_V4/html/c_method.html) for details.

## [How to identify which variant is installed](/docs/mdsdk/knowledge-base/why-oesis-detects-a-product-but-only-patches-some-of-variants#how-to-identify-which-variant-is-installed)

There are several ways to identify which variant of a product is installed:

1. **Signature ID and name.** OESIS detection results (e.g., `DetectProducts`) include the matched signature ID and name. The signature name usually encodes the variant — for example, *Mozilla Firefox UWP* vs. *Mozilla Firefox x64*, or *Microsoft Teams* vs. *Microsoft Teams work or school*.
2. **Uninstall registry hive.** Inspect the product's installation metadata via OESIS product-information methods (e.g., `GetProductInfo`): an uninstall entry under `HKEY_LOCAL_MACHINE` indicates a per-machine install, while `HKEY_CURRENT_USER` indicates a per-user install.
3. **Uninstall string.** An `msiexec`-based uninstall string indicates an MSI install; a path to an uninstaller executable indicates an EXE-based install; Microsoft Store apps do not appear under the classic uninstall keys at all.

## [Variants not covered by the categories above](/docs/mdsdk/knowledge-base/why-oesis-detects-a-product-but-only-patches-some-of-variants#variants-not-covered-by-the-categories-above)

The categories above cover the structural reasons a variant cannot be patched (Microsoft Store distribution, discontinued variants, and end-of-life release lines). For any other product variant where you need patching, please raise a request with OPSWAT Support. Patching coverage is continuously expanded, and support for additional variants is prioritized based on customer demand — customer requests are the primary driver for adding new patchable signatures.

When raising a request, include the product name, the matched signature ID/name from the detection result, and the OS and architecture; this allows the request to be scoped to the exact variant you need.
