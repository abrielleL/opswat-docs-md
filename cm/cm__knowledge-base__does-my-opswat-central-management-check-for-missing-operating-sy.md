<!-- source: https://www.opswat.com/docs/cm/knowledge-base/does-my-opswat-central-management-check-for-missing-operating-sy -->

# Does My OPSWAT Central Management check for missing operating system patches and hotfixes?

Yes, it does.

My OPSWAT Central Management is designed to check the operating systems on each of your managed endpoints for any missing patches or hotfixes.

To do this, OPSWAT uses the relevant operating system’s classification of mandatory and optional patches, where **Mandatory** generally means **Critical** or **Severe**.

If missing patches or hotfixes are detected, the My OPSWAT Central Management Console will report these missing patches, along with their severity and timestamps, under **Inventory>Devices>Relevant Device>Device Details View>Missing Patches**, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/r6m5vdqey4w7irp1xfqw7r2kr90507t58xf8fb6fh3cthg4vfkawcslm96hlnnx8.png)

To remedy a missing patch or hotfix issue, visit the device **Remediation Page**, where you will find remediation requirements as well as a link to detailed remediation instructions.

![](https://uploads.developerhub.io/prod/97qW/6exsqdukryfe9ztatlb6xyiu29cbmifqlwloiteh0i3vna35sxz3h94f1a523g8c.png)

![](https://uploads.developerhub.io/prod/97qW/kg4puswt7tl8lpoy11aieo1rh0hn1byl72uc7zrkoci77p1f0vgoz76lak5fsfzq.png)

If no patches or hotfixes are missing, **Patch Management** will show an **Up To Date** status.

> **Pro Tip:**
>
> To configure the frequency of scans and reports on missing patches, go to **Console>Settings>Global>Device Agents**.
>
> Here, you will find an adjustable time setting under the **Compliance Report** heading, as illustrated in the screenshot below.
>
> Once configured, click **Save** to apply your settings.

![](https://uploads.developerhub.io/prod/97qW/x9adhv3rtwpt7lydmzyrn56bd7xgfsv6xidtb3bb7uqc8gc2r8boy407qao9c7n6.png)

> **Support:**
>
> For any queries, concerns or issues regarding **Scanning, Reporting And Remediation Of Missing Operating System Patches And Hotfixes**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
