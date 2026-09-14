<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management -->

# How OESIS Supports Bulletin for Patch Management

This article explains how bulletins are designed in OESIS patch management. A bulletin is a named security advisory that groups one or more individual patches under a single stable identifier, giving management servers an advisory-level view of patch data. The article covers what bulletins are, where they come from, how bulletin IDs are formatted, the `bulletin.json` catalog schema, and how bulletins link to the patch aggregation files.

## [What is a bulletin?](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#what-is-a-bulletin)

Patch data in OESIS has traditionally been organized by product and version. That works for "keep me current" scenarios, but IT administrators and compliance tools think in terms of releases and advisories: "is this Patch Tuesday update deployed?", "which endpoints are missing this Adobe APSB fix?". A **bulletin** provides that missing handle.

A bulletin groups one or more individual patches under a single identifier, together with the advisory metadata administrators expect: title, summary, severity, release date, CVE list, and reference links. Instead of tracking patches by raw product/version, bulletins let a management server organize, filter, and display patch data by advisory, the same way an IT administrator reads a Microsoft Patch Tuesday announcement or an Adobe APSB notice. This gives you:

- **A stable identity for each release.** Compliance policies and audit queries can reference a bulletin ID directly instead of reconstructing releases from raw version strings.
- **Advisory-level grouping.** A single release that ships multiple patches (for example, several product versions) is represented as one bulletin, so consumers no longer need to reassemble the release themselves.

## [Where bulletin data lives](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#where-bulletin-data-lives)

Bulletin data is published in `bulletin.json`, a server-side file in the Analog package under `server/`:

analog.zip
└── server/
└── bulletin.json

**Platforms:** Windows, macOS, Linux.

`bulletin.json` is the bulletin catalog: it is what a server-side consumer reads to understand which bulletins exist, what they cover, and which patches belong to each. It works alongside the existing patch aggregation files, which continue to carry the full patch metadata (see How bulletins relate to other Analog files below).

## [Bulletin sources](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#bulletin-sources)

Each bulletin has a `source` field identifying where it came from:

| `source` | Meaning | Example IDs |
| --- | --- | --- |
| `vendor` | Advisory published by the vendor and consumed as-is (Microsoft KB, Adobe APSB) | `MS26-0512-5087065`, `APSB26-12` |
| `opswat` | OPSWAT-tracked third-party software release | `CHROME-2605`, `FIREFOX-2606` |

## [Bulletin ID format](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#bulletin-id-format)

### [Microsoft KB — `MS<YY>-<MMDD>-<KB>`](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#microsoft-kb--msyy-mmdd-kb)

Example: `MS26-0512-5087065`, which is KB5087065 from the May 12, 2026 Patch Tuesday.

All KBs from the same Patch Tuesday share the `MS26-0512` prefix, so consumers can group them without a separate field.

### [Adobe APSB — `APSB<YY>-<NN>`](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#adobe-apsb--apsbyy-nn)

Example: `APSB26-12`

### [OPSWAT third-party — `<PRODUCT_CODE>[<PLATFORM_SUFFIX>]-<YYMM>`](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#opswat-third-party--product_codeplatform_suffix-yymm)

Each OPSWAT bulletin covers a single product on a single platform for a given month.

| Platform | Suffix | Example |
| --- | --- | --- |
| Windows | *(none)* | `CHROME-2605` |
| macOS | `MAC` | `CHROMEMAC-2605` |
| Linux | `LINUX` | `CHROMELINUX-2605` |

Common product codes:

| Product | Code |
| --- | --- |
| Google Chrome | `CHROME` |
| Mozilla Firefox | `FIREFOX` |
| Oracle Java 8 | `JAVA8` |
| Oracle JDK 11 | `JDK11` |
| VMware Tools | `VMWARETO` |

## [Schema](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#schema)

### [Bulletin metadata](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#bulletin-metadata)

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| `id` | string | yes | Unique bulletin identifier |
| `source` | string | yes | `"vendor"` or `"opswat"` |
| `vendor` | string | no | Vendor name, `vendor` bulletins only (e.g. `"microsoft"`, `"adobe"`) |
| `kb` | string | no | KB article, Microsoft bulletins only (e.g. `"KB5058481"`); not present for Adobe APSB bulletins |
| `title` | string | yes | Human-readable bulletin title |
| `summary` | string | yes | Brief description |
| `severity` | string | yes | See Severity values below |
| `release_date` | string | yes | `MM/DD/YYYY` |
| `cves` | string[] | yes | CVE identifiers |
| `references` | string[] | yes | Reference URLs (may be `[]`) |
| `patches` | array | yes | Individual patches covered by this bulletin (see Patch metadata below) |

### [Patch metadata](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#patch-metadata)

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| `product_name` | string | yes | Product name |
| `version` | string | yes | Patch version |
| `platform` | string | yes | `"windows"`, `"macos"`, or `"linux"` |
| `patch_uuid` | string | no | Links to `patch_aggregation_v2.json` or `patch_system_aggregation_v2.json`; when absent, use `product_name` and `version` to identify the patch |

### [Severity values](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#severity-values)

For `vendor` bulletins, severity comes from the vendor's published rating. For `opswat` bulletins, severity is the highest severity among the CVEs listed in `cves`.

| Value | Meaning |
| --- | --- |
| `critical` | Remote code execution or unauthenticated privilege escalation |
| `important` | Privilege escalation, spoofing, or significant data disclosure |
| `moderate` | Limited exploitability or partial impact |
| `low` | Minimal or difficult-to-exploit vulnerability |
| `unrated` | No severity assigned by vendor |

## [How bulletins relate to other Analog files](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#how-bulletins-relate-to-other-analog-files)

Bulletins sit above the patch data; they reference patches rather than duplicate them. `bulletin_ids` appears in two other server-side files, linking patches back to their bulletins:

| File | How it references bulletins |
| --- | --- |
| `patch_aggregation_v2.json` | Each third-party patch entry carries `"bulletin_ids": [...]` |
| `patch_system_aggregation_v2.json` | Each Windows system patch entry carries `"bulletin_ids": [...]` |

Use `patch_uuid` from `patches[]` to look up full patch metadata in those files.

## [Usage](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#usage)

### [Group patches by advisory](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#group-patches-by-advisory)

1. Load `bulletin.json`.
2. Filter by `source`, `id` prefix, or `severity`.
3. Display `title`, `severity`, `cves`, and `references` per bulletin.
4. Expand `patches[]` to list affected products and versions.

### [Look up a bulletin from a known patch](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#look-up-a-bulletin-from-a-known-patch)

patch_aggregation_v2.json
└── bulletin_ids: ["FIREFOX-2606"]
│
▼
bulletin.json (id == "FIREFOX-2606")
└── cves, severity, references, patches[]
### [Look up patch detail from a bulletin](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#look-up-patch-detail-from-a-bulletin)

bulletin.json
└── patches[].patch_uuid == "84fca5d0-..."
│
▼
patch_aggregation_v2.json (patch_uuid == "84fca5d0-...")
└── version, download packages, requires_restart, ...
## [Examples](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#examples)

### [OPSWAT bulletin (third-party)](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#opswat-bulletin-third-party)

{
"id": "FIREFOX-2606",
"source": "opswat",
"title": "Mozilla Firefox Security Update 06/2026",
"summary": "Mozilla Firefox patches for 06/2026",
"severity": "important",
"release_date": "06/16/2026",
"cves": ["CVE-2026-10701", "CVE-2026-10702", "CVE-2026-12289"],
"references": [],
"patches": [
{
"product_name": "Mozilla Firefox",
"version": "151.0.3",
"platform": "windows",
"patch_uuid": "84fca5d0-cdd6-58c0-a709-be997f0ab74e"
},
{
"product_name": "Mozilla Firefox",
"version": "152.0",
"platform": "windows",
"patch_uuid": "a40134d2-a7cd-5e35-834c-e43109c0a084"
}
]
}
### [Microsoft bulletin (vendor)](/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management#microsoft-bulletin-vendor)

{
"id": "MS26-0210-5075999",
"source": "vendor",
"vendor": "microsoft",
"kb": "KB5075999",
"title": "Windows Security Update - February 2026 (KB5075999)",
"summary": "Fixes 21 CVEs (Critical) for Windows products",
"severity": "critical",
"release_date": "02/10/2026",
"cves": ["CVE-2026-20846", "CVE-2026-21222", "CVE-2026-21231"],
"references": [
"https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB5075999",
"https://support.microsoft.com/help/5075999"
],
"patches": [
{
"product_name": "Windows 10 Version 1607 for x64-based Systems",
"version": "10.0.14393.8868",
"platform": "windows",
"patch_uuid": "015b898e-3a63-4bc3-8007-b54e5d6ca0b4"
}
]
}Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
