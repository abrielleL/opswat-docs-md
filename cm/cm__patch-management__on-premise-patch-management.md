<!-- source: https://www.opswat.com/docs/cm/patch-management/on-premise-patch-management -->

# On-Premise Patch Management

This guide explains how Patch Management works in My OPSWAT Central Management (On-Premises), including the two available versions and how to switch between them.

My OPSWAT Central Management (On-Premises) supports two versions:

| Version | Supports | Availability |
| ---- | ---- | ---- |
| [Air-Gapped Patching - Classic Patch Settings](https://www.opswat.com/docs/cm/patch-management/air-gapped-patching) | Legacy patch configuration and workflows | Supported on My OPSWAT Central Management version 10.3.2512.2391 or later |
| [Air-Gapped Patching - New Patch Management](https://www.opswat.com/docs/cm/patch-management/air-gapped-patching---new-patch-management) | Unified patch lifecycle management with dashboards, deployments,  | - **Fresh installations on version 10.6.2605 or later**: the new Patch Management solution is enabled by default - **Upgraded installations to version 10.6.2605 or later**: administrators can manually switch between Classic Patch Settings and New Patch Management |

## How to switch between the two versions

You can move between two versions using the following methods:

- Open the **User Profile Menu** in the top-right corner and select **Switch to New Patch Management** or **Switch to Classic Patch Settings**.
- If the** Introducing New Patch Management **banner is shown, click **Try Now**.

![](https://uploads.developerhub.io/prod/97qW/ccn0aw7er7lbfy7fwtwk5jgdig3ud1qmd0j5i6xv3vs7543kajhm1xv14k7qn1a8.png)

![](https://uploads.developerhub.io/prod/97qW/89gngg98tc5i62mz7gi9j2u0nki39t0zvrzxhzdj4v5dfb7wi5z2dzgjcxqldd5m.png)

Note  After switching to the new Patch Management solution, MetaDefender Endpoints stop executing existing Classic Patch Settings configurations until you switch back. If you switch back to Classic Patch Settings, all MetaDefender Endpoints stop executing Patch Deployment policies until the new Patch Management solution is enabled again.
