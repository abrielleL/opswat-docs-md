<!-- source: https://www.opswat.com/docs/cm/patch-management/bulletin-and-data-source -->

# Bulletin and Data Source

Patch Management shows the full security story behind every patch, not just that an update exists. Two new pieces of information make this possible: Bulletin and Data Source.

## How We Collect Bulletin Information?

For detailed information about how bulletin is collected, please see [How OESIS Supports Bulletin for Patch Management](https://www.opswat.com/docs/mdsdk/knowledge-base/how-oesis-supports-bulletin-for-patch-management) document.

## What Is a Bulletin?

A Bulletin is the security advisory behind a patch. It describes what the patch fixes, how serious the issue is, and which vulnerabilities it closes. One bulletin can cover several patches at once.  For example, a single Microsoft advisory may apply to every edition and system architecture it was released for.

Note The Bulletin ID is shown for OS patches only, it does not appear on application patches.

## What Is a Data Source?

Data Source shows where a patch record's information came from, such as OPSWAT or WinGet. It describes the patch itself, not the advisory attached to it. Because of this, it is separate from who issued the bulletin and does not change based on which vendor makes the product.

## Where You'll See This

The Missing Patches list displays the data source for every OS and application patch. However, the bulletin is shown for OS patches only.

|  |  |
| ---- | ---- |
| OS Missing Patches | ![](https://uploads.developerhub.io/prod/97qW/w8r3hgaxe1hsipbr1o7dvmdwlnb70xpnx7dbi8ptvhywc85r1xw6ltp1uz6wtgw7.png) - Select ⓘ icon next to a Bulletin to view all the detailed information - Click View Patches to see all patches that belong to a specific bulletin ![](https://uploads.developerhub.io/prod/97qW/7k60lrsohghq2k9qcf28sh009uigja2k7gmut7lzbckw5lxmsz9kshv3tvp9ux2u.png) |
| Application Missing Patches | ![](https://uploads.developerhub.io/prod/97qW/tzltnf0k1sdamusm7ez8sqi2m8p1w9sbs9eubn73l11iu8qjmqvepqm7y0kdzrlr.png) |
| Patch Details | The patch details also show the data source, and the bulletin ID for OS patches: ![](https://uploads.developerhub.io/prod/97qW/rw1sl10hku75dmytxis4uo1ph8uubvwmlxguyhap9x9qs9fcai0n7zqbi03pda3v.png) |

## Current Availability

Bulletin and Data Source metadata is only captured for patch records from May 26, 2026 onward. Patches recorded before this date will not have this metadata.
