<!-- source: https://www.opswat.com/docs/my/release-notes/v2026-1-3 -->

# v2026.1.3 - Mar 30

## My OPSWAT Portal v2026.1.3.2

| **Version** | 2026.1.3.2 |
| ---- | ---- |
| **Release date** | April 10th, 2026 |
| **Release Summary** | This release includes enhancements to OAuth Application Management and other general bug fixes and enhancements. |

Enhancements OAuth Application management is now organization-level. Only organization super admins and admins can create and manage OAuth applications.

Further details at [OAuth Application](https://www.opswat.com/docs/my/others/oauth-application)

## My OPSWAT Portal v2026.1.3.1

| **Version** | 2026.1.3.1 |
| ---- | ---- |
| **Release date** | April 3rd, 2026 |
| **Release Summary** | This release includes general bug fixes and enhancements. |

## My OPSWAT Portal v2026.1.3.0

| **Version** | 2026.1.3.0 |
| ---- | ---- |
| **Release date** | March 30th, 2026 |
| **Release Summary** | This release introduces the first public API for license data and system enhancements. |

## New Features

### OAuth API for License and Deployment Information

We now support an OAuth-based API that allows customers to retrieve a license’s deployment history from My OPSWAT Portal.

![](https://uploads.developerhub.io/prod/JYvy/vpxrcfxn87cg1f856oaaphfyos1y3bxzsd4f4fw04r9lxo3hje7odpdjxkwf2z7q.png)

Customers can register an OAuth application in the Portal to obtain access tokens for API authentication, and retrieve license information and active deployment IDs associated with each license key via API.

![](https://uploads.developerhub.io/prod/JYvy/yxf08ukhkttt9bhvad68wdfy5u37u80fh67lgh66k307a3okrug7785d90luffhw.png)

**Access path:** Account menu > OAuth Application

**Further reading:** [OAuth Application](https://www.opswat.com/docs/my/others/oauth-application)

## Enhancements

### Improved License Monitoring

The number of near-capacity and expiring licenses for each organization is now presented in a list format instead of a bar chart. This change allows you to view the numbers directly without the need to hover, making it easier to access the information at a glance.

![](https://uploads.developerhub.io/prod/JYvy/3905w4ee700ukq411d8n8daf8e9mcwpmyueopodm9svh4ep8so8su04fuujbt8ac.png)
